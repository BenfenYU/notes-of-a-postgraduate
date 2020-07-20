# Adversarial Training For Sketch Retrieval

## Main Task and Contribution

To show that GANs can be used **to learn a representation suitable** for visual search. We apply this  novel idea to the Merchant Mark dataset, and compare two GAN architectures.

The question is whether such Generative Adversarial Networks can learn feature representations suitable for retrieval in a way that matches human perception.

Without the level of labeling and examples required for non-adversarial training approaches. This broadens the scope of deep networks to problems of perceptually similar retrieval in the absence of class labels, a problem that is increasingly of interest in heritage collections of images.

## Model Architecture

Common GAN. 

- sketch-GAN: larger filters in shallower layers of D and deeper levels pf G.
- thin-GAN: small filters and reduce the number of filters to balance the parameter number of two models.

Training methods is also common.

After training, D without its last classification layer is used to be an encoder.

## Model Comparing

- shift invariance: 

  The step size in sliding the search box will affect the computational feasibility of the search. If a representation used for search is invariant to larger shifts, then a sliding box search can be performed with a larger step size, making the search more efficient.

  ![image-20200712134730286](/home/bf/.config/Typora/typora-user-images/image-20200712134730286.png)

- invariance to rotation:

  At each 0.5 degree increment, the samples were encoded and the similarity score between the rotated sample and the sample at 0 degrees was calculated. The similarity score used was the normalised dot product, since this was also the measure used for retrieval.

  ![image-20200712134630412](/home/bf/.config/Typora/typora-user-images/image-20200712134630412.png)

- invariance to scale:

  At each increment of 0.05, the scaled sample was encoded and a similarity score was calculated between the scaled samples and the sample at scale 1. 

![image-20200712135028892](/home/bf/.config/Typora/typora-user-images/image-20200712135028892.png)

## Question unsolved

- No exact evaluation methods, they just judge methods by human eyes.
- They do not compare retrieval results with other models (baseline and state-of-the-art models)

# SketchMate: Deep Hashing for Million-Scale Human Sketch Retrieval

## Main Task and Contribution

We propose a deep hashing framework for sketch retrieval that, for the first time, works on a multi-million scale human sketch dataset.

In this paper, we combine RNN stroke modeling with conventional CNN under a dual-branch setting to learn better sketch feature representations. 

 (i) For the first time, we introduce the problem of sketch hashing retrieval on a multi-million scale human sketch dataset, and propose a deep hashing network that directly accommodates the key characteristics of human sketch.  (ii) We propose a novel multi-branch CNN-RNN architecture that specifically encodes the temporal ordering information of sketches to learn a more fine-grained feature representation.(iii) We design a novel hashing loss to accommodate the abstract nature of
sketches, especially on such a large dataset where noise is also present.

- a deep hashing framework for sketch retrieval 
- a novel multi-branch CNN-RNN architecture
- a novel hashing loss

## Model Architecture

![image-20200712170044548](/home/bf/.config/Typora/typora-user-images/image-20200712170044548.png)

### Fusion of Two Branches

cat(cnn branch , rnn branch) -> fc with sigmoid, f -> be transformed to the hashing code, b.

![image-20200712181446665](/home/bf/.config/Typora/typora-user-images/image-20200712181446665.png)

### Learning Objective

- cross entropy loss(CEL) for sample pairs K on L categories softmax.

![image-20200712182028718](/home/bf/.config/Typora/typora-user-images/image-20200712182028718.png)

- quantization loss to reduce the error caused by quantization-encoding.

![image-20200712193353565](/home/bf/.config/Typora/typora-user-images/image-20200712193353565.png)

- sketch center loss

  1. pretraining cnn and rnn separately for sketch recognition task with softmax cross entropy loss only.

  2. obtain class feature center c by calculating the mean of the hashing feature f for the noise-removal sketches (detailed later) of that class based on the pretrained model. 

  3. using center c we define sketch center loss.

     ![image-20200712193718100](/home/bf/.config/Typora/typora-user-images/image-20200712193718100.png)

- full learning objective

![image-20200712194018963](/home/bf/.config/Typora/typora-user-images/image-20200712194018963.png)

### Noise Removal

Given a category of sketch, we can get entropy for each sketch and the overall entropy distribution on a category basis. We empirically find that keeping the middle 90% of each category as normal samples gives us best results.

![image-20200712193932341](/home/bf/.config/Typora/typora-user-images/image-20200712193932341.png)

### Training Procedure

![image-20200712194606844](/home/bf/.config/Typora/typora-user-images/image-20200712194606844.png)

## Experiments

### Datasets and Settings

- for evaluation,  we form our query and retrieval gallery set by randomly choosing 100 and 1000 sketches from each category. 
- for faster training, we reduce to two states by eliminating the sketch termination signal for faster training, leading each time-step input to the RNN module a four-dimensional input.

## Questions

- Why do they use sketch center loss and what does the loss really mean?
- What does hashing really benefit to retrieval and recognition?
- Need to make or read a summary on loss functions, and is it helpful that we have more different loss functions in one model if we regard loss function as constraint?