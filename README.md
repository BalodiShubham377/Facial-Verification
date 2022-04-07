# Facial-Verification
This project has been used to implement 
Facial Recognition using Siamese Network architecture.

# One Shot Learning
Deep neural networks are really good at learning from high dimensional data like images or spoken language, but only when they have huge amounts of labelled examples to train on. Humans on the other hand, are capable of one-shot learning - if you take a human who’s never seen a spatula before, and show them a single picture of a spatula, they will probably be able to distinguish spatulas from other kitchen utensils with astoundingly high precision.

Recently there have been many interesting papers about one-shot learning with neural nets and they’ve gotten some good results and one of them is using Siamese Network.

## Siamese Network

It is an approach to getting a neural net to do one-shot classification is to give it two images and train it to guess whether they have the same category. Then when doing a one-shot classification task described above, the network can compare the test image to each image in the support set, and pick which one it thinks is most likely to be of the same category. So we want a neural net architecture that takes two images as input and outputs the probability they share the same class.

If we just concatenate two examples together and use them as a single input to a neural net, each example will be matrix multiplied(or convolved) with a different set of weights, which breaks symmetry. Sure it’s possible it will eventually manage to learn the exact same weights for each input, but it would be much easier to learn a single set of weights applied to both inputs. So we could propagate both inputs through identical twin neural nets with shared parameters, then use the absolute difference as the input to a linear classifier - this is essentially what a siamese net is. Two identical twins, joined at the head, hence the name

![siamese](https://user-images.githubusercontent.com/76276009/162209728-ad81e86a-1b08-4a0e-ac98-88032ed5b17e.png)

The output is squashed into [0,1] with a sigmoid function to make it a probability. We use the target t = 1 when the images have the same class and t = 0 for a different class. It’s trained with logistic regression. This means the loss function should be binary cross entropy between the predictions and targets. There is also a L2 weight decay term in the loss to encourage the network to learn smaller/less noisy weights and possibly improve generalization

When it does a one-shot task, the siamese net simply classifies the test image as whatever image in the support set it thinks is most similar to the test image
