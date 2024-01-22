# NextBrain - Case 5
This repository contains data that is consumed by the [NextBrain project](https://github.com/UCL/NextBrain). This data corresponds to case 5. For the source code of this project refer to the main [NextBrain repo](https://github.com/UCL/NextBrain).

## Data structure
This brain specimen has been cut into 49 blocks including cerebrum, cerebellum and brain stem. The histology-related data is organised following a numbered list of blocks, from 1 to 49. 

The struture of the dataset is as follows:
- [Histology](#histology)
- [High-resolution histology](#histology_hr)
- [MRI](#mri_rotated)
- [Util files](#utils)


<div id='histology'/>
  
### Histology

This directory (_histology_) contains data on the histology space at 0.1 mm in-plane resolution. The spacing between histology slices is either 250 μm for blocks that included subcortical structures in the forebrain, medial structures of the cerebellum and brainstem structures or 500 μm for the other blocks. This resolution has been used in the 3D histology reconstruction pipeline. 
For each block, we provide the following data:
 - __slices_LFB__: histology slices stained using LFB and non-linearly aligned to the corresponding MRI section (.jpg extension).
 - __slices_HE__: histology slices stained using HE and non-linearly aligned to the corresponding MRI section (.jpg extension).
 - __slices_MRI__: masked MRI sections corresponding to histology slices (.jpg extension).
 - __slices_labels__: structure labels delineated on the LFB slice and non-linearly aligned to the corresponding MRI section (.png extension).
 - __slices_labels_npz__: structure labels delineated on the LFB slice and non-linearly aligned to the corresponding MRI section (.npz extension).
 - __matrix.txt__: affine matrix that relates the block (stack of images) and the MR image.

<div id='histology_hr'/>
  
### High-resolution histology

This directory (_histology_hr_) contains data on the histology space at 1.9844 μm in-plane resolution. The spacing between histology slices is either 250 μm for blocks that included subcortical structures in the forebrain, medial structures of the cerebellum and brainstem structures or 500 μm for the other blocks.
For each block, we provide the following data:
 - __slices_LFB__: histology slices stained using LFB and non-linearly aligned to the corresponding MRI section (.jpg extension).
 - __slices_HE__: histology slices stained using HE and non-linearly aligned to the corresponding MRI section (.jpg extension).
 - __slices_MRI__: masked MRI sections corresponding to histology slices (.jpg extension).
 - __slices_labels__: structure labels delineated on the LFB slice and non-linearly aligned to the corresponding MRI section (.png extension).
 - __slices_labels_npz__: structure labels delineated on the LFB slice and non-linearly aligned to the corresponding MRI section (.npz extension).
 - __matrix.txt__: affine matrix that relates the block (stack of images) and the MR image.


<div id='mri_rotated'/>
  
### MRI
This directory (_mri_rotated_) contains data on the MRI space. We use a T2-weighted sequence at 400 μm isotropic resolution with the following parameters: R = 500 ms, TEeff = 69 ms, BW = 558 Hz/Px, echo spacing = 4.96 ms, echo train length = 58, 10 averages, acquisition time for each average = 547 s.

The data in this directory consists of:
- __mri.nii.gz__: MRI scan.
- __slices\_{axial/sagittal/coronal}__: orthogonal views of the 3D MRI volume (.png extension);
- __indices.nii.gz__: volume containing the the corresponding block number of each voxel on the MRI scan.
- __indices\_{axial/sagittal/coronal}__: 2D integer image containing the block number corresponding to each voxel on the MRI slice (.npy extension);
- __matrices{/_hr}__: affine matrices that relate the MRI volume with each block on the histology space for both resolutions. Each of these matrices is the inverse of the matrices found in the histology directories.


<div id='utils'/>
  
### Util files

- __histologyDimensionsKey.json__: metadata corresponding to the *histology* directory. It contains the image size and number of slices for each block, as well as the orientation of the acquisition.
- __histologyHRDimensionsKey.json__: metadata corresponding to the *histology_hr* directory. It contains the image size and number of slices for each block, as well as the orientation of the acquisition.
- __mriDimensionsKey.json__: metadata corresponding to the *mri* directory. It contains the image size and number of slices in each orthogonal direction.
- __image_ontology_hierarchical.json__: it contains the label ontology used to delinate brain structures split into two levels: the first one correspond to high-level ROI structures while the second contains the nuclei in each structure. Moreover, it contains the centroid voxel of each nuclei on MRI space $(x_m, y_m, z_m)$ and on histological space $(x_h, y_h, z_h)$
	

## How to relate MRI and histology?
In this repo we store a set of matrices to relate the MRI volume (or the orthogonal views) to each histology slice in any of its available contrasts: LFB, HE or labels.
The matrices stored under the _mri_rotated_ directory are defined from the MRI spatial coordinates to histology (in both resolutions). An example of how to relate MRI and histology is shown in the following picture,.

![alt text](https://github.com/UCL/NextBrain-Case5/blob/main/mri2histo.svg?raw=true)

On the contrary, matrices stored under _histology_ and _histology_hr_ directores are defined from the histology slice to the MRI volume, and the process would be the opposite to the one shown in the figure. Thus, one initially fixes the block and slice numbers and the spatial histology coordinates and then compute the MRI space coordinates. Finally, to compute the physical RAS coordinates, one can use the header of the nifti file _mri.nii.gz_.


## Additional BrainAtlas patient data:
* [Case 1](https://github.com/UCL/NextBrain-Case1)
* [Case 2](https://github.com/UCL/NextBrain-Case2)
* [Case 3](https://github.com/UCL/NextBrain-Case3)
* [Case 4](https://github.com/UCL/NextBrain-Case4)


