# A Simple Summary

### What

There are many different task in sketch, however, for one dataset, what the models really need is to find a representation(feature) vector which can represent distribution of the whole dataset. Then we can add some module after the feature vector for specific task.

### Methods

- CNN

  1. CNN is very powerful, however,  it can't fit some character of sketch very well.
  2. CNN has arrived a high accuracy.
  3. Research using CNN with unsupervised learning on sketch is still blank.

  ![image-20200719132759655](images/image-20200719132759655.png)

- RNN

  1. Temporal points as input maybe make no or little sense, especially after attention was invented. 
  2. Some simple information captured by RNN can still be captured by CNN (such as ResNet50).
  3. Considering the human, we don't care about every points of a sketch, points will be organized in our brain and I think this is structural information.

- GNN

  1. Learning structural knowledge, combining with self-supervised learning is perfect. 
  2. Like human, we can't recognize the pattern if the points or strokes are random and noisy.

- Transformer&Bert

  1. Seq2seq, the sequence is still composed of points, sketch bert has arrive their upper bound.
  2. Self-supervised learning is their shining point.

![image-20200719110041642](../notes/images/image-20200719110041642.png)

![image-20200719110146114](images/image-20200719110146114.png)

![image-20200719110213750](images/image-20200719110213750.png)

![image-20200719110248631](images/image-20200719110248631.png)

![image-20200719110315471](images/image-20200719110315471.png)

![image-20200719110329754](images/image-20200719110329754.png)

![image-20200719110434153](images/image-20200719110434153.png)

![image-20200719110457815](images/image-20200719110457815.png)

![image-20200719110530310](images/image-20200719110530310.png)

![image-20200719110550073](images/image-20200719110550073.png)

### Characteristics of Sketch

- no background information
- drawn casually
- vector (temporal points and stroke)
- highly abstract
- highly sparsely

### Idea

- how to embedding sketch? There are image, image&points sequence, points sequence and graph
- how to fix the casualty sketch drawing? how to make model capable of dealing with randomness? add random sample from N(0,1) to some layers?
- recognition and retrieval have been highly studied (especially using RNNs), maybe it's time to translate application direction.
- graph, self-supervision, serve sketch as image and create a new extractor (like convolution filter as common images)
- reference other strategies of deep learning (unsupervised, transfer learning ...)
- is there 3d-graph alive? (laugh)