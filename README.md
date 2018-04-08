# Teachable Machine Boilerplate
**[Try this demo](https://googlecreativelab.github.io/teachable-machine-boilerplate/)**

This is a small boilerplate project that demonstrates how to use [deeplearn.js](https://deeplearnjs.org) to create projects 
like [Teachable Machine](https://teachablemachine.withgoogle.com/). The code shows how you can create setup a KNN classifier that can be trained live in the browser on a webcam image. It is intentionally kept very simple so it can provide a starting point for new projects.

Behind the scenes the image from the webcam is being processed by a small neural network called [SqueezeNet](https://github.com/DeepScale/SqueezeNet). This network is trained to recognize all sorts of classes from the ImageNet dataset, and is optimized to be really small, making it useable in the browser. Instead of reading the prediction values from the SqueezeNet network, we take the second to last layer in the neural network and feed it into a KNN ([k-nearest neighbors](https://en.wikipedia.org/wiki/K-nearest_neighbors_algorithm)) classifier that allows you to train your own classes. 

The benefit of using the SqueezeNet model instead of feeding the pixel values directly into the KNN classifier is that we use the high level abstractions that the neural network has learned in order to recognize the ImageNet classes. This allows us with very few samples to train a classifier that can recognize things like smiles vs frown, or small movements in your body. This technique is called [Transfer Learning](https://en.wikipedia.org/wiki/Transfer_learning).

Deeplearn.js has a built in model for doing this. It's called [KNN Image Classifier Model](https://github.com/PAIR-code/deeplearnjs/tree/master/models/knn_image_classifier), and this boilerplate code shows how to easily use it.

If you are interested in using this with [p5.js](https://p5js.org/), ITP has created a similar example that you can find [here](https://ml5js.github.io/docs/knn-image-example.html).

## Use code
To use the code, first install the JavaScript dependencies by running  

```
npm install
```

Then start the local budo web server by running 

```
npm start
```

This will start a web server on [`localhost:9966`](http://localhost:9966). Try and allow permission to your webcam, and add some examples by holding down the buttons. 

## Quick Reference
A quick overview of the most important function calls in the deeplearn.js [KNN Image Classifier](https://github.com/PAIR-code/deeplearnjs/tree/master/models/knn_image_classifier)

- `KNNImageClassifier(numClasses, k)`: The constructor takes an argument of how many classes you want to train and recoginize, and a `k` value that is the number of neighbors looked at when doing the classification. A value of `10` can be a good starting point.

- `.load()`: Downloads the SqueezeNet model from the internet, and setups the model.

- `.addImage(image, classIndex)`: Adds an image to the specific class training set

- `.clearClass(classIndex)`: Clears a specific class for training data

- `.predictClass(image)`: Runs the prediction on the image, and returns (as a Promise) the class index and confidence score. 

See the full implementation [here](https://github.com/PAIR-code/deeplearnjs/blob/master/models/knn_image_classifier/knn_image_classifier.ts)
