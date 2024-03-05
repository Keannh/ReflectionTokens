# Self Referential Tokens

## Standard Training
<img src="https://github.com/Keannh/ReflectionTokens/blob/main/Images/StandardGPT.png?raw=true" alt="drawing" width="400"/>

## Training with Reflection Tokens
<img src="https://github.com/Keannh/ReflectionTokens/blob/main/Images/WithReflectionToken.png?raw=true" alt="drawing" width="600"/>

# Abstract



# Motivation

1. Hypothesis: The more data == better performance paradigm holds only when the weights receive many different individual gradients of similar magnitude and similar direction in every trainstep. Thus, increasing the amount of gradients is a good thing given that the data is meaningful.
2. The backward pass on the \<Reflection\> token provides meaningful feedback because it allows the model to reflect and refer to its previous calculations, thus correcting errors.
3. During inference the amount of \<Reflection\> token can be adapted, and thus more difficult tokens can be given more computation. I see many possible implementations here.
