# Teachable Machine Boilerplate
This is a small boilerplate project that demonstrates how to use [deeplearn.js](https://deeplearnjs.org) to create projects like [Teachable Machine](https://teachablemachine.withgoogle.com/). The code shows how you can create setup a KNN classifier that can be trained live in the browser on a webcam image.

Behind the scenes the image from the webcam is being processed by a small neural network called Squeezenet. This network is trained to recognize all sorts of classes from the imagenet dataset, and is optimized to be really small making is useable in the browser. Instead of reading the prediction values from the squeezenet network, we instead take the second to last layer in the neural network and feed it into a KNN ([k-nearest neighbors](https://en.wikipedia.org/wiki/K-nearest_neighbors_algorithm)) classifier that allows you to train your own classes. 

The benefit of using the squeezenet model instead of feeding the pixel values directly into the KNN network is that we use the high level abstractions that the neural network has learned in order to recognize the Imagenet classes. This allows us with very few samples to train a classifier that can recognize things like smiles vs frown, or small movements in your body. 

## Use code
To use the code, first install the javascript dependencies by running  

```
npm install
```

Then start the local budo webserver by running 

```
npm start
```

This will start a webserver on [`localhost:9966`](http://localhost:9966). Try and allow permission to your webcam, and add some examples by holding down the buttons. 