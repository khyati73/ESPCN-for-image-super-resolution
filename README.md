# ESPCN-for-image-super-resolution
Efficient sub-pixel convolutional neural networks can be used for both images and videos.  ESPCN (Efficient Subpixel CNN), is a model that reconstructs a high-resolution version of an image given a low-resolution version. The ‘array’ of image upscaling filters are learned by efficient sub-pixel convolution layers.
Why ESPCN:
1) Firstly, the input of SRCNN is a bicubic low resolution image which is an approximation of High resolution image. These smoothing effects can lead to misinterpretation of the actual high resolution image. Also, the interpolation is quite time consuming.
2) SRCNN is a layered architecture, therefore making it a very simple model. So, it was quite fascinating what will be the result of a more deep model.
3) There was another common question, that is, what could be the result if the parameters such as scaling factors were changed. Can it yield better results?
4) The issue of using bicubic interpolation was dealt with by creating a model that adaptively increases the resolution. FSRCNN is the model that uses the technique of upsampling operation known as deconvolution or transposed convolution. 
5) FSRCNN had its own problems. It used nearest neighbour interpolation in which there was a chance of points in upsampled features repeating several times. 
6) This problem was dealt with by expanding the channels of the output features for storing the extra points to obtain the high resolution output through a specific mapping criterion.


The general pipeline followed in conventional SR techniques begins with mapping the LR image to HR usually employing bicubic interpolation, and then learning the model in higher dimensional space.
This pipeline has larger computational requirements, and hence ESPCN perform feature extraction in the LR space. After the features are extracted, ESPCN uses a sub-pixel convolution layer at the very end to aggregate LR feature maps and simultaneously perform projection to high dimensional space to reconstruct the HR image. Feature processing in LR space significantly reduces the memory and computational requirements. The bicubic interpolation used in SRCNN and nearest neighbour interpolation used in FSRCNN is replaced with the interpolation that pads the sub-pixels with zeroes.
We have used a small dataset to train our model: BSDS500 dataset.
Downloading the dataset: used the keras.utils.get_file utility to retrieve the dataset.
The training and validation datasets are created from image_dataset_from_directory.
Images are rescaled to take values between the range of [0,1]
dataset_url = "http://www.eecs.berkeley.edu/Research/Projects/CS/vision/grouping/BSR/BSR_bsds500.tgz"
