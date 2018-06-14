# Repeatabilty of Multiparametric Prostate MRI Radiomics Features

This repository contains data and code accompanying our publication(s) on "Repeatabilty of Multiparametric Prostate MRI Radiomics Features"

[TBA links to paper(s)]

## Data

### Exctracted Features

The [TBA] folder contains all extracted features we used in the study.

#### File Format Description

The files are in CSV format. Each row contains all features extracted for one image and mask combination. The organizatin and naming of the columns is directly taken from [pyradiomics](https://github.com/Radiomics/pyradiomics). We just added a few columns containing some additional meta information about the image/mask from which the features were derived. 

The first few colums contain general info about the feature extraction (prefixed with "general_info"):

| Column Name (w/o prefix) | Meaning |
|--------------------------|---------|
| BoundingBox	             | The bounding box considered around the mask |
| EnabledImageTypes	       | Indicates which pre-filtering options were activated for the extraction |
| GeneralSettings	         | Indicates which general settings were activated for the extraction (e.g. normalization, resampling, ...) |
| ImageHash	               | Unique identifier of the image |
| ImageSpacing	           | Voxel spacing |
| MaskHash	               | Unique identifier of the mask |
| NumpyVersion	           | Numpy version used by pyradiomics |
| PyWaveletVersion	       | PyWavelet version used by pyradiomics |
| SimpleITKVersion	       | SimpleITK version used by pyradiomics |
| Version	                 | Pyradiomics version used for the extraction |
| VolumeNum	               | Number of zones (connected components) within the mask for the specified label |
| VoxelNum                 | Number of voxels in the mask |

Afterwards follow the colums for each feature. The feature column names follow this pattern: 

*[pre-filter]\_[feature group]\_[feature name]*

For example:
* original\_shape\_Volume
* wavelet-HH\_glcm\_JointEnergy

At the end we added a few colums with additional meta information:

| Column Name              | Meaning |
|--------------------------|---------|
| study	                   | Identifying the study this image belongs to |
| series	                 | Identifying the series this image belongs to |
| canonicalType	           | Type/modality of the image (e.g. ADC, T2w, SUB) |
| segmentedStructure	     | Type of structure segmented by the mask |

#### Filename Pattern Description

The filenames of the feature data CSVs also contain some additional meta information about their content. The jupyter notebook for genearting figures will parse this information and save it with the statistics it creates from the feature data (so you don't really have to worry about these to much).

The following table explains the different "codes" in the filename of a feature CSV file:

| File name contains       | Meaning |
|--------------------------|---------|
| FullStudySettings	       | Simply indicates that the extraction settings were according to this study (we also did smaller studies) |
| noNormalization          | Indicates that the default pyradiomics whole-image normalization was deactivated |
| 2d/3D 	                 | Indicates if texture features were computed in 2D or 3D |
| biasCorrected	           | Indicates that we applied bias correction to the T2w images before processing them with pyradiomics |
| TP2Registered	           | Indicates that for the T2w images we didn't use the first manual segmentation but used registration to transfer the second timepoint masks to the first timepoint (see paper for more info) |
| MuscleRefNorm            | Indicates that we normalized the T2w images against a consistent reference region in muscle tissue |
| T2AX                     | Contains only results for T2w images |
| bin10/bin15/bin20/bin40  | Bin size used for texture feature computation |




## Jupyter Notebooks

The jupyter notebooks require Python >= 3.6. 

### Feature extraction

The [TBA notebook name] contains the code that performed the feature extraction. You will also need the image data and the [pyradiomics library](https://github.com/Radiomics/pyradiomics). Check the paper for information on how to get the image data. Note that it is not guaranteed that a different version of pyradiomics will create the same results for all features. Check the paper as well as the feature data files for the version that was used for this study.

This notbeook requires a custom Python library wich you should download and put in a location where it will be found by Python (e.g. point the PYTHONPATH environment variable to the parent folder):
* [mpReviewUtils](https://github.com/michaelschwier/mpReviewUtils) (only required for the feature extraction notebook)

### Figure generation

The [TBA notebook name] contains the code that was used to generate the figures for the pre-print paper [TBA link]. It also contains additional figures and can be used as a good basis to create your own additional figures from the data.
