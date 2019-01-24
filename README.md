# Semantic Segmentation
![Semantic Segmentation 1](./runs/1543024307.0486972/umm_000030.png)
![Semantic Segmentation 2](./runs/1543024307.0486972/uu_000053.png)
![Semantic Segmentation 3](./runs/1543024307.0486972/uu_000098.png)
![Semantic Segmentation 4](./runs/1543024307.0486972/umm_000053.png)
![Semantic Segmentation 5](./runs/1543024307.0486972/uu_000099.png)
![Semantic Segmentation 6](./runs/1543024307.0486972/uu_000089.png)
### Introduction
In this project, you'll label the pixels of a road in images using a Fully Convolutional Network (FCN).  We started by loading a frozen pre_trained VGG16 graph, and unfreezing specific layers to be converted from dense layers, to 1D Convolutional to create a fully convolutional encoder for our street image data.

We change the dense layers to 1D convolutions because 1D preserves the depth/spatial information, while dense layers do not.


### Setup
##### GPU
`main.py` will check to make sure you are using GPU - if you don't have a GPU on your system, you can use AWS or another cloud computing platform.
##### Frameworks and Packages
Make sure you have the following is installed:
 - [Python 3](https://www.python.org/)
 - [TensorFlow](https://www.tensorflow.org/)
 - [NumPy](http://www.numpy.org/)
 - [SciPy](https://www.scipy.org/)
##### Dataset
Download the [Kitti Road dataset](http://www.cvlibs.net/datasets/kitti/eval_road.php) from [here](http://www.cvlibs.net/download.php?file=data_road.zip).  Extract the dataset in the `data` folder.  This will create the folder `data_road` with all the training a test images.

### Start

##### Run
Run the following command to run the project:
```
python main.py
```
**Note** If running this in Jupyter Notebook system messages, such as those regarding test status, may appear in the terminal rather than the notebook.


 ### Tips
- The link for the frozen `VGG16` model is hardcoded into `helper.py`.  The model can be found [here](https://s3-us-west-1.amazonaws.com/udacity-selfdrivingcar/vgg.zip)
- The model is not vanilla `VGG16`, but a fully convolutional version, which already contains the 1x1 convolutions to replace the fully connected layers. Please see this [forum post](https://discussions.udacity.com/t/here-is-some-advice-and-clarifications-about-the-semantic-segmentation-project/403100/8?u=subodh.malgonde) for more information.  A summary of additional points, follow.
- The original FCN-8s was trained in stages. The authors later uploaded a version that was trained all at once to their GitHub repo.  The version in the GitHub repo has one important difference: The outputs of pooling layers 3 and 4 are scaled before they are fed into the 1x1 convolutions.  As a result, some students have found that the model learns much better with the scaling layers included. The model may not converge substantially faster, but may reach a higher IoU and accuracy.
- When adding l2-regularization, setting a regularizer in the arguments of the `tf.layers` is not enough. Regularization loss terms must be manually added to your loss function. otherwise regularization is not implemented.
