# Brain-Tumor-Classification

In this notebook, I've used **CNN** to perform Image Classification on the Brain Tumor dataset.<br>
Since this dataset is small, if we train a neural network to it, it won't really give us a good result.<br>
Therefore, I'm going to use the concept of **Transfer Learning** to train the model to get really accurate results.

<img width="1067" alt="image" src="https://user-images.githubusercontent.com/57068021/169701570-27cdf80a-c9d8-4c46-aa73-3b9098ad3d21.png">

## Data Preparation

* We start off by appending all the images from the directories into a Python list and then converting them into numpy arrays after resizing it.
![alt text](https://github.com/pberjon/Brain-Tumor-Classification/blob/main/labels_sample_image.png)

* Dividing the dataset into Training and Testing sets.
* Performing **One Hot Encoding** on the labels after converting it into numerical values

## Transfert Learning 
Deep convolutional neural network models may take days or even weeks to train on very large datasets.

A way to short-cut this process is to re-use the model weights from pre-trained models that were developed for standard computer vision benchmark datasets, such as the ImageNet image recognition tasks. Top performing models can be downloaded and used directly, or integrated into a new model for your own computer vision problems.

In this notebook, I'll be using the **EfficientNetB0** model which will use the weights from the **ImageNet** dataset.

The include_top parameter is set to *False* so that the network doesn't include the top layer/ output layer from the pre-built model which allows us to add our own output layer depending upon our use case!

<img width="1017" alt="image" src="https://user-images.githubusercontent.com/57068021/169701665-d660c037-476a-44e7-9678-16e74f789fa7.png">

**GlobalAveragePooling2D** -> This layer acts similar to the Max Pooling layer in CNNs, the only difference being is that it uses the Average values instead of the Max value while *pooling*. This really helps in decreasing the computational load on the machine while training.
<br><br>
**Dropout** -> This layer omits some of the neurons at each step from the layer making the neurons more independent from the neibouring neurons. It helps in avoiding overfitting. Neurons to be ommitted are selected at random. The **rate** parameter is the liklihood of a neuron activation being set to 0, thus dropping out the neuron

**Dense** -> This is the output layer which classifies the image into 1 of the 4 possible classes. It uses the **softmax** function which is a generalization of the sigmoid function.

We then compile our model.

<img width="1017" alt="image" src="https://user-images.githubusercontent.com/57068021/169701698-a853682a-61cf-473d-baf4-710d3c0998d0.png">

**Callbacks** -> Callbacks can help you fix bugs more quickly, and can help you build better models. They can help you visualize how your model’s training is going, and can even help prevent overfitting by implementing early stopping or customizing the learning rate on each iteration.<br><br>
By definition, "A callback is a set of functions to be applied at given stages of the training procedure. You can use callbacks to get a view on internal states and statistics of the model during training."

In this project, I'll be using **TensorBoard, ModelCheckpoint and ReduceLROnPlateau** callback functions.

## Model Training

<img width="1017" alt="image" src="https://user-images.githubusercontent.com/57068021/169701735-ab6e21bd-6bae-4afc-9e43-26f79ca3c09b.png">

<img width="851" alt="image" src="https://user-images.githubusercontent.com/57068021/169701778-13794a3a-b912-4cf5-a71b-9cee45d4111e.png">

## Prediction

I've used the argmax function as each row from the prediction array contains four values for the respective labels. The maximum value which is in each row depicts the predicted output out of the 4 possible outcomes.
So with argmax, I'm able to find out the index associated with the predicted outcome.

## Evaluation

<img width="529" alt="image" src="https://user-images.githubusercontent.com/57068021/169701819-8856df3e-5df5-4380-8317-75d4ee4ca349.png">

<img width="757" alt="image" src="https://user-images.githubusercontent.com/57068021/169701839-3bbc7285-417d-4bfa-b774-aa851aac6f8d.png">

## Conclusion

In this project, I performed Image Classification with the help of CNN using Transfer Learning which gave an accuracy of around 98%.<br>
I also made widgets which can make predictions on an image from your local machine:

<img width="1090" alt="image" src="https://user-images.githubusercontent.com/57068021/169701891-8d305300-5a2a-48c1-b73a-dda550dbe42e.png">

