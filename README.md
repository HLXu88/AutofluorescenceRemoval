# AutofluorescenceRemoval
This repository is for referring autofluorescence removal pipelines

Multiplex immunohistochemistry (mIHC) technologies enable the detection of multiple markers on a single tissue section, providing valuable quantitative data for understanding disease heterogeneity and molecular profiling. Various mIHC techniques, including chromogenic mIHC, TSA-based fluorescence mIHC, metal-based mIHC, cyclic mIHC/IF, and DNA barcoding-based mIHC, have been developed, each with its own advantages and limitations. To address this issue, we investigated an enhanced open-source method using digital processing to eliminate AF. By providing a robust and automated solution for AF elimination, this method enhances the precision of mIHC analysis and facilitates large-scale studies, ultimately contributing to a deeper understanding of disease mechanisms and the development of targeted therapies.

## Step 1: Overlay Three Biomarkers
Image acquisition to obtain original 16-bit grayscale TIFF images using the fluorescent microscope. Use “GrayToColor” modules to transfer invisible 16-bit grayscale images to visible RGB images
![Step1](https://github.com/user-attachments/assets/666c029b-48dd-489c-a25b-9fa807d7818b)

## Step 2: Identification of target proteins and AF
Place the raw grayscale images into six separate image processing pipelines. 
![Figure-pip-1-2](https://github.com/user-attachments/assets/db327b43-e01b-4858-bced-2ffef8c4b4d1)

Use “IdentifyPrimaryObjects” modules with advanced settings to identify objects of AF, cell nuclei, epithelial/tumor cells, COX-2, PTGER4, and PIK3CA
![Figure-pip-4](https://github.com/user-attachments/assets/410f0b86-eba5-499c-ae20-edeeb0bfe9ac)
![Step2Sample](https://github.com/user-attachments/assets/4f6b2f15-310d-4b85-883d-8f53eeff29a5)

Use "FilterObjects” modules to remove the small objects (noise) less than 40 pixels (in area value) for three biomarker images and objects less than 20 pixels (in area value) for DAPI and Pan CK images.
![Figure-pip-5-6](https://github.com/user-attachments/assets/5ffecbef-d72e-4dc8-8ec4-1a90c0a49945)

Use "SaveImages" module to save identified objects' images.
![Figure-pip-10](https://github.com/user-attachments/assets/98e9ab75-ceff-45ec-97a2-0ac65472ff81)

## Step 3: 
## Step 4: Eliminated AF objects
Input the six “ObjectsIdentified” images into an image measurement pipeline for continued image processing.

Use “ConvertImageToObjects” module to convert loaded visible images to calculable objects.

Use “ExpandObjects” module to expand AF objects for 3 pixels for fully removing tissue foldings.

Use “MaskObjects” modules to remove AF objects, tissue folding, and edge effects by overlaying AF images with other fluorophore images to obtain five AF-free images for each sample. The white arrows indicate the eliminated AF objects. 
