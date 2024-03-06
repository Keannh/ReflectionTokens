# Self Referential Tokens

## Standard Training
<img src="https://github.com/Keannh/ReflectionTokens/blob/main/Images/StandardGPT.png?raw=true" alt="drawing" width="400"/>

## Training with Reflection Tokens
<img src="https://github.com/Keannh/ReflectionTokens/blob/main/Images/WithReflectionToken.png?raw=true" alt="drawing" width="600"/>

# Abstract
Introduce \<Reflection\> tokens during training randomly dispersed in the input text. On those \<Reflection\> tokens the model should predict the same label as the last real token. That way, the model can attend to its own prediction for a token and improve upon it. During inference \<Reflection\> tokens may also be added in places that require strong reasoning and reflection abilities.


# Motivation

1. Hypothesis: The more data == better performance paradigm holds only when the weights receive many different individual gradients of similar magnitude and similar direction in every trainstep. Thus, increasing the amount of gradients is a good thing given that the data is meaningful.
2. The backward pass on the \<Reflection\> token provides meaningful feedback because it allows the model to reflect and refer to its previous calculations, thus correcting errors.
3. During inference the amount of \<Reflection\> token can be adapted, and thus more difficult tokens can be given more computation. I see many possible implementations here.

# Previous Work

Goyal at al. use a very similar idea but do not provide a loss signal for their \<Reflection\> (or in their case \<Pause\>) Tokens. 
I think this
1. wastes gradient information
2. Introduces a vanishing gradient problem. For the sequence t1 t2 pause pause t3 for instance I suspect that the gradient information that goes directly from t3 to t2 is disproportionally larger than the signal that goes from t3->pause->pause->t2 (out of the same reason that problem exists in RNNs, though I am not 100% about the math). Thus the pause tokens add no meaningful gradient information to the weights.

# Implementation Details
It might be of value to limit the attention of further tokens to the real tokens and not the \<Reflection\> tokens in order not to increase the computational overhead. I.e. for the input (t1 t2 \<Reflection\> t3 t4) t3 would only attend to t1 and t2 and not to \<Reflection\> . 

# Alternatives
Instead of introducing a new \<Reflection\> token, one could also just repeat the last token as an input. Thus, a possible input and loss signal might be
(t1 t2 t2 t3) -> (t2 t3 t3 t4)

# References

@misc{PauseTokens,
      title={Think before you speak: Training Language Models With Pause Tokens}, 
      author={Sachin Goyal and Ziwei Ji and Ankit Singh Rawat and Aditya Krishna Menon and Sanjiv Kumar and Vaishnavh Nagarajan},
      year={2023},
      eprint={2310.02226},
      archivePrefix={arXiv},
      primaryClass={cs.CL}
}
