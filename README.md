# Creating Datasets of 3D Buildings from 2D Images

## About 

This study demonstrates a method to create large databases of 3-D buildings in any style using the recently released Neural Reflectance Surfaces (NeRS) approach. Developed at Carnegie Melon University in 2021 by Jason Zhang Et. al, NeRS is an algorithmic method that converts in-the-wild, sparse-view image datasets of objects into geometrically and texturally accurate water-tight reconstructions.  Given the increasing demand for and general scarcity of 3-D data for deep learning research and applications, this approach provides an excellent means of meeting this demand as applied to objects that have been only sparsely photographed.

![](images/boyko.gif)
![](images/transcar.gif)
![](images/boyko_3.gif)
![](images/hutsul_2.gif)

## Why NeRS?

In ideal conditions, building images can be easily reconstructed into highly accurate 3D representations by using photograpmmetry software like Bently System’s “ContextCapture” or Epic Game’s “Reality Capture” programs. However, these systems, like many others, require hundreds or thousands of images of a target object to reconstruct it in 3D. However, there are many situations where collecting hundreds of images is impossible. For example, when the target building is innaccesible and cannot be photographged further due to geographic distance or privatye ownership, when a building no longer exists, or when there are hundreds or thousands of target buildings and capturing additional photographs of each one becomes impossible due to limited time, budget, or human capacity constraints. In this situation, NeRS provides an excellent solution to obtain 3D representation of buildings that have only been sparsely photographed.

## Case Study

As case study, and as the first demonstrations of the NeRS process being applied to architecture, we demonstrate the creation of a custom dataset of 331 3-D digital models of wooden churches from Carpathian Mountain regions in and around Ukraine.  Given that no more than a dozen 3-D models of these buildings exist, the Carpathian Wooden Churches of this region are an ideal candidate for this demonstration.  We then showcase a method to augment the dataset from 331 buildings to 5,627 buildings to satisfy the training dataset requirements of typical deep learning models.

![](images/intro_banner.png)

## Project Page

An expanded description of this model implimentation can be found on its project page here:

[www.michaelhasey.com/deep-vernacular-summary](www.michaelhasey.com/deep-vernacular-summary)

## Table of Contents

- [Dataset](#Dataset)
- [Approach](#Approach)
- [Implementation](#Implementation)
- [Performance](#Performance)
- [References](#References)
- [Citation](#Citation)

## Approach

Constructing a dataset of 3D churches using NeRS and then preparing it for DL-based experiments requires a nine-stage work-flow (Figure 90): 1) a broad search for churches and acquisition of exterior church images; 2) selection of the final images showcasing all exterior sides of each church; 3) editing the images to remove occlusions, correct perspective distortions, and compensate for missing images; 4) creating image masks representing the location and outline of the church; 5) estimating image angles between the camera and the church; 6) estimating the general dimensions of the churches (length, width, and height) ; 7) reconstructing a high-quality detailed 3D mesh object, 8) Augmenting the data from 331 churches to 5627 models, 9) converting the models to SDF voxel format. 

![](images/image_pair.png)

### Step 1:  Searching for Churches & Collecting Imagery

The wooden churches used in this research reside within the mountainous, foothill and water-shed region of the Carpathian Mountain region of Central Europe.  In order to build the dataset, digital images of over 400 churches were manually searched for and collected over a one month period.  In total, over 10,000 images were collected, representing 409 unique churches from the central Carpathian Mountain region showcasing a wide range of distinct styles and sub-styles.  Images were acquired from a number of online resoures, including, but not limited to, Google Earth, various academics and domain experts, various blogs, and multiple image repositories that specialize in historic architecture of this region.

![](images/image_pair.png)

### Step 2:  Image Pre-Processing

Images for each church needed to be carefully pre-processed and  prepared for 3-D reconstruction. First, the final images required for the 3D reconstruction process need to be selected. Then, some images were altered in order to ensure their associated church was accurately reconstructed in 3D. For example, images occasionally had to be manually edited or constructed to provide the front or rear elevations. Next, object masks needed to be provided for each individual image. Then, both the horizontal and vertical camera angle between the camera and the church for each image was manually recorded to a JSON file. Next, a custom script was created to automatically duplicate images and horizontally flip them to represent the other side of the building. Finally, the dimensions of a shape template corresponding to the estimated approximate size of each church must be determined 

![](images/select_cut.png)

### Step 3:  Reconstructing Churches in 3-D

Once all images have been preprocessed and their corresponding JSON files complete, the final stage of the reconstruction pipeline (Figure 113) was reached and each church was reconstructed from the images as a high-quality detailed mesh object using the NeRS algorithm.  To reconstruct each church a remote computing cluster containing 4 GPUs (NVidia GeForce GTX Titan X with 12 GB of VRAM) was used to expedite this process. Once completed, the reconstruction quality of each church was manually inspected. Out of the original 409 churches, 96 could not be recon-structed due to insufficient imagery.

![](images/channels.png)

The dataset of reconstructed churches includes 313 individual buildings (Figure 115, 116). The dataset were then automatically augmented from 313 buildings to 5,627 buildings using an algorithm that made slightly different copies of each building through a series of random rotation and scaling transformations. 

### Step 4: Augment Dataset using Synthetic Data

In order to sufficiently train the DL network and extract a reasonable latent space distribution, where latent space is a representation of abstracted data where similar data points are clustered closer to-gether, the dataset needed to be augmented from 313 buildings to 5,627 buildings. Data augmenta-tion is common technique if the dataset is insufficiently large to train a DL-model and helps prevent overfitting [32]. Overfitting is when a model begins to memorize hyper-specific features of the data, rather than more useful general features of the data that might help better describe it as a whole. To avoid overfitting, the dataset was augmented to be 17X its original size by making 17 copies of each building, with each copy being slightly different from the next through a series of transformations such as rotation and randomly scaling. To expedite this process, a custom script and data pipeline was created in Grasshopper, a parametric design software used to create and manipulate 3D geometry. 

![](images/neagtive.png)

## References

This project was completed as part of Carnegie Melon University's Learning Based Image Synthesis course 16 726 taught by Jun-Yan Zhu in Spring of 2021.

## Citation

If you find this project useful in your research, please consider citing:

``` 
@misc{mhasey2021,
    title={Image Blending Tool},
    author={Michael Hasey},
    year={2021},
}
```
