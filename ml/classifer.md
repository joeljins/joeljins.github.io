---
layout: default
title: Classifier
permalink: /classifier
---
# Building a Furniture Classifier
*Source [code](https://github.com/joeljins/cs380_assignments) kept private to respect Drexel's academic integrity policies.*

<br>
## A Quick Demo:
<iframe src="https://drive.google.com/file/d/1u7e3RaxquNBade_y7fLtYcnuK0RdKR1S/preview" width="640" height="480" allow="autoplay"></iframe>

<br>
## Dataset:

The dataset consists of a series of images from Ikea's furniture catalogue. Each image is a single bed, chair, sofa, or table with a white background. Provided with a sample classifier and an autoencoder, I was tasked with modifying them to build a set of stacked autoencoders and a final classifier. Because certain images from the could reasonably be mistaken as others, I aimed for the accuracy of the final classifier to be arond 95%. 

<br>
## Autoencoders:

The autoencoders reproduces the input as output. It consists of an encoder, which transforms the input into a latent representation, and the decoder, which transforms the latent representation into the output. This output should be in the same form as the input. Three autoencoders with the same layers are stacked to create a classifier network for the final classifier. 

### Encoder
The encoder needs to do a single convolution + max pooling. Using the Torch module, we layer them into the encoder. The dimensions of the second encoder are one-half of the first encoder, and the dimensions of the third encoder are one-half of the second encoder.

The second and third autoencoders consist of the same layers, but the data is encoded by the prior enconder(s).

```
self.encoder = Model(
            input_shape=(self.BATCH_SIZE, 3, dimension, dimension),
            layers=[
                nn.Conv2d(3, n_kernels, kernel_size=3, padding=1),
                nn.ReLU(),
                nn.MaxPool2d(kernel_size=2),
            ]
        )
````

### Decoder

The decoder needs to undo the convolution, so we layer the operations below into it. 

```
self.decoder = Model(
        input_shape=(self.BATCH_SIZE, n_kernels, dimension/2, dimension/2),
        layers=[
            nn.ConvTranspose2d(n_kernels, 3, kernel_size=3, stride=2,
                                padding=1, output_padding=1),
            nn.Sigmoid(), # nn.RelU() for the second and third decoders
        ]
    )
```

<br>
## Training
Each of the autoencoders are trained for 100 epochs. 
```
 > python3 ae1.py 100
 > python3 ae2.py 100
 > python3 ae2.py 100
```

<br>
## Classifier:
The final classifier has the following layers, with each of the three encoders serving as a layer:
```
layers=[
                self.encoder1,
                self.encoder2,
                self.encoder3,
                nn.Flatten(),
                nn.Dropout(p=0.1),
                nn.Linear(n_kernels * 8 * 8, 256),
                nn.ReLU(),
                nn.Dropout(p=0.1),
                nn.Linear(256, 64),
                nn.ReLU(),
                nn.Linear(64, 4),
            ]
```
The classifier is trained for 100 epochs:
```
> python3 cl1.py 100
```

<br>
## The Final Results:

<div class="container1">

    <style>
        .container1{
            display: flex;
            flex-direction: row;
            gap: 5px;
            align-content: center;
        }
        .box{
            display: flex;
            flex-direction: column;
            gap: 5px;
        }
    </style>

        <div class="box">
            <h3> Autoencoder #1 </h3>
            <img src="assets\images\classifier\ae1pt1.webp" width="200" height="200">
            <img src="assets\images\classifier\ae1pt1.webp" width="200" height="200">
        </div>

        <div class="box">
            <h3> Autoencoder #2 </h3>
            <img src="assets\images\classifier\ae2pt1.webp" width="200" height="200">
            <img src="assets\images\classifier\ae2pt1.webp" width="200" height="200">
        </div>

        <div class="box">
            <h3> Autoencoder #3 </h3>
            <img src="assets\images\classifier\ae3.pt1.webp" width="200" height="200">
            <img src="assets\images\classifier\ae3pt2.webp" width="200" height="200">
        </div>

</div>

<br>

<h3> Classifier </h3>
<div class="container2">

    <style>
        .container2{
            display: flex;
            flex-direction: row;
            gap: 5px;
        }
    </style>

    <img src="assets\images\classifier\classifier_accuracy.png" width="400" height="200">
    <img src="assets\images\classifier\classifier_results.webp" width="200" height="200">

</div>
