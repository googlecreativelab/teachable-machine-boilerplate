# Teachable Machine Boilerplate
This is a small boilerplate project that demonstrates how to use [tensorflow.js](https://github.com/tensorflow/tfjs-models) to create projects like [Teachable Machine](https://teachablemachine.withgoogle.com/). The code shows how you can create a KNN classifier that can be trained live in the browser on a webcam image. It is intentionally kept very simple so it can provide a starting point for new projects.

Behind the scenes, the image from the webcam is being processed by an activation of [MobileNet](https://github.com/tensorflow/tfjs-examples/tree/master/mobilenet). This network is trained to recognize all sorts of classes from the imagenet dataset, and is optimized to be really small, making it useable in the browser. Instead of reading the prediction values from the MobileNet network, we instead take the second to last layer in the neural network and feed it into a KNN ([k-nearest neighbors](https://en.wikipedia.org/wiki/K-nearest_neighbors_algorithm)) classifier that allows you to train your own classes. 

The benefit of using the MobileNet model instead of feeding the pixel values directly into the KNN classifier is that we use the high level abstractions that the neural network has learned in order to recognize the Imagenet classes. This allows us with very few samples to train a classifier that can recognize things like smiles vs frown, or small movements in your body. This technique is called [Transfer Learning](https://en.wikipedia.org/wiki/Transfer_learning).

Tensorflow has a built in model for doing this. It's called the [KNN Classifier](https://github.com/tensorflow/tfjs-models/tree/master/knn-classifier), and this boilerplate code shows how to easily use it.

## Use code
To use the code, first install the Javascript dependencies by running  

```
npm install
```

Then start the local budo web server by running 

```
npm start
```

This will start a web server on [`localhost:9966`](http://localhost:9966). Try and allow permission to your webcam, and add some examples by holding down the buttons. 

## Quick Reference - KNN Classifier
A quick overview of the most important function calls in the tensorflow.js [KNN Classifier](https://github.com/tensorflow/tfjs-models/tree/master/knn-classifier).

- `knnClassifier.create()`: Returns a KNNImageClassifier.

- `.addExample(example, classIndex)`: Adds an example to the specific class training set.

- `.clearClass(classIndex)`: Clears a specific class for training data.

- `.predictClass(image)`: Runs the prediction on the image, and returns an object with a top class index and confidence score. 

See the full implementation [here](https://github.com/tensorflow/tfjs-models/blob/master/knn-classifier/src/index.ts)

## Quick Reference - MobileNet
A quick overview of the most important function calls we use from the tensorflow.js model [MobileNet](https://github.com/tensorflow/tfjs-models/tree/master/mobilenet).

- `.load()`: Loads and returns a model object.

- `.infer(image, endpoint)`: Get an intermediate activation or logit as Tensorflow.js tensors. Takes an image and the optional endpoint to predict through.

See the full implementation [here](https://github.com/tensorflow/tfjs-models/blob/master/mobilenet/src/index.ts)