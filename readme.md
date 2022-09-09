# Face Recognition Experiments on the Face Recognition from Mugshots Database (FRMDB)

This repository contains the source code of the experiments presented in
> P. Contardo, P. Sernani, S. Tomassini, N. Falcionelli, M. Martarelli, P. Castellini, A.F. Dragoni, *The Face Recognition from Mugshots Database: a Dataset to Test the Use of Mugshots from Multiple Points of View for Identification*.

The paper is currently under review for the publication in the [Sensors](https://www.mdpi.com/journal/sensors) journal.

The source code of the experiments on the datasets is contained in a Jupyter notebook, available in the “notebooks” directory of this repository. The notebook is "[Face_Recognition_with_the_Face_Recognition_from_Mugshots_Database_(FRMDB).ipynb](notebooks/Face_Recognition_with_the_Face_Recognition_from_Mugshots_Database_(FRMDB).ipynb)"

Specifically, the experiments are **accuracy tests of two different Convolutional Neural Networks (CNNs)**, pre-trained on the [VGGFace](https://www.robots.ox.ac.uk/~vgg/data/vgg_face/) and [VGGFace2](https://github.com/ox-vgg/vgg_face2) databases, on the **Face Recognition from Mugshots Database (FRMDB)**.

The FRMDB is publicly available in a dedicated GitHub repository:

>[LINK HERE](#)

Specifically, we tested VGG16 and ResNet50, using the configurations presented in

>Parkhi, O.M.; Vedaldi, A.; Zisserman, A. Deep face recognition. British Machine Vision Association 2015. [PDF](https://www.robots.ox.ac.uk/~vgg/publications/2015/Parkhi15/parkhi15.pdf)

for **VGG16**, and in 

>Cao, Q.; Shen, L.; Xie, W.; Parkhi, O.M.; Zisserman, A. VGGFace2: A Dataset for Recognising Faces across Pose and Age. In Proceedings of the 2018 13th IEEE International Conference on Automatic Face & Gesture Recognition (FG 2018), 2018, pp. 67–74. [PDF](https://www.robots.ox.ac.uk/~vgg/publications/2018/Cao18/cao18.pdf)

for **ResNet50**. Instead of running again the training on VGG16 and ResNet50, we used the weights and the models available in

><https://github.com/rcmalli/keras-vggface>

Such repository includes the Keras conversion of the original CAFFE networks and weights.

## Data Description

The experiments are based on the FRMDB images and videos. The FRMDB is available in the following public repository: 
>[LINK HERE](#)

The database includes images and videos of 42 subjects. Specifically, for each subject there are:

- 28 mugshots, i.e., 28 972x544 JPEG image takens from different points of views with the subject posing during the acquisition.

- 5 security cameras videos, taken from 5 points of views. In addition, a mosaic video including all the 5 clips at the same time is available. The 5 videos are 60 fps 352x288 H.264 encoded clips (the container format is matroska - mkv). The frame size of the mosaic is 1280x720.

In the experiments we used the face manually cropped from the mugshots and from 1 frame of each security video. The cropped faces are available in the FRMDB repository.

## Experiments

The experiments perform the **comparison** the embedding of the faces of each subject in the **security cameras** with different **set of mugshots** available in the FRMDB. The embeddings are computed using **VGG16** and **ResNet50**.

The experiments consists of **8 different tests** to identify the subjects in the security camera images:
- *Test F*, using the **frontal mugshot** (33, according to the code used in the FRMDB) of each subject for the comparison.
- *Test F-L1-R1*, using the **frontal** mugshot (33) and the mugshots **to the left and to the right of the frontal** (i.e., 23 and 43).
- *Test 1*, using the **frontal** mugshot (33) and **the right profile** (53) of each subject.
- *Test 2*, using the **frontal** mugshot (33), the **right** profile (53), and the **left** profle (13) of each subject.
- *Test 3*, using the mugshots of the ***Test F-L1-R1*** and ***Test 2*** (i.e., 13, 23, 33, 43, 53)
- *Test 4*, adding the images with **highest left** (03) and **right** (63) angles to ***Test 3***.
- *Test 5*, which adds **all the images 30° above the subject** (i.e., 02, 12, 22, 32, 42, 52, 62) to the mugshots of ***Test 4***.
- *Test 6*, which uses **all the 28 mugshots** available for each subject in the FRMDB.

The following images visualize the subset of mugshots available in each test (the image is related to the subject 033 of the FRMDB).

![The sets of mugshots used in each test.](images/tests.gif)

The following table lists all the mugshot available in each test for each subject as a couple (*h*, *v*) where *h* is the angle from which the mugshot was taken on the horizontal plane, and *v* is the angle on the vertical plane.

| **Test**     | **Mugshots**                                                                                                                                                                                                                                                                                                                                                        |
|:-------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Test F       | (0°, 0°)                                                                                                                                                                                                                                                                                                                                                            |
| Test F-L1-R1 | (0°, 0°), (-45°, 0°), (45°, 0°)                                                                                                                                                                                                                                                                                                                                     |
| Test 1       | (0°, 0°), (90°, 0°)                                                                                                                                                                                                                                                                                                                                                 |
| Test 2       | (0°, 0°), (90°, 0°), (-90°, 0°)                                                                                                                                                                                                                                                                                                                                     |
| Test 3       | (0°, 0°), (90°, 0°), (-90°, 0°), (45°, 0°), (45°, 0°)                                                                                                                                                                                                                                                                                                               |
| Test 4       | (0°, 0°), (135°, 0°), (-135°, 0°), (90°, 0°), (-90°, 0°), (45°, 0°), (45°, 0°)                                                                                                                                                                                                                                                                                      |
| Test 5       | (0°, 0°), (135°, 0°), (-135°, 0°), (90°, 0°), (-90°, 0°), (45°, 0°), (45°, 0°), (0°, 30°), (135°, 30°), (-135°, 30°), (90°, 30°), (-90°, 30°), (45°, 30°), (45°, 30°)                                                                                                                                                                                               |
| Test 6       | (0°, 0°), (135°, 0°), (-135°, 0°), (90°, 0°), (-90°, 0°), (45°, 0°), (45°, 0°), (0°, 30°), (135°, 30°), (-135°, 30°), (90°, 30°), (-90°, 30°), (45°, 30°), (45°, 30°), (0°, 60°), (135°, 60°), (-135°, 60°), (90°, 60°), (-90°, 60°), (45°, 60°), (45°, 60°), (0°, -30°), (135°, -30°), (-135°, -30°), (90°, -30°), (-90°, -30°), (45°, -30°), (45°, -30°)          |

For each test, we measured the capability of VGG16 and ResNet50 to identify the subject in each image from the security cameras, by registering if **the subject** was **included** in the **top-1**, **top-3**, **top-5**, and **top-10 most similar mugshots**, and in the **top-1**, **top-3**, **top-5**, and **top-10 nearest identities**. To evaluate the similarity between a face in a mugshot and a face in the image from a security camera, we use the **Euclidean distance** as the similarity measure between the **two face embeddings**. Given such similarity criterion, we measure the accuracy as follows:
- For the **most similar identities**, we compute the accuracy as the **number of security camera images** for which the **correct subject** was in the **top-1**, **top-3**, **top-5**, and **top-10** nearest identities **over the total** number of security camera images.
- For the **most similar mugshots**, we compute the accuracy as the **number of security camera images** for which the **correct subject** was in the **top-1**, **top-3**, **top-5**, and **top-10** most similar mugshots **over the total** number of security camera images.
Obviously, the top-1 identity and the top-1 mugshot overlap.

The following images shows a frame for each of the security camera videos related to the subject 033 of the FRMDB

<p align="center">
	<img src="images/cam-1.jpg" alt="Cam 1 example">
	<img src="images/cam-2.jpg" alt="Cam 2 example">
	<img src="images/cam-3.jpg" alt="Cam 3 example">
</p>

<p align="center">
	<img src="images/cam-4.jpg" alt="Cam 4 example">
	<img src="images/cam-5.jpg" alt="Cam 5 example">
</p>
 