# AutofluorescenceRemoval
This repository is for referring autofluorescence removal pipelines

Multiplex immunohistochemistry (mIHC) technologies enable the detection of multiple markers on a single tissue section, providing valuable quantitative data for understanding disease heterogeneity and molecular profiling. Various mIHC techniques, including chromogenic mIHC, TSA-based fluorescence mIHC, metal-based mIHC, cyclic mIHC/IF, and DNA barcoding-based mIHC, have been developed, each with its own advantages and limitations.To address this issue, we investigated an enhanced open-source method using digital processing to eliminate AF. By providing a robust and automated solution for AF elimination, this method enhances the precision of mIHC analysis and facilitates large-scale studies, ultimately contributing to a deeper understanding of disease mechanisms and the development of targeted therapies.
## Step 1 Identification of target proteins and AF
Put the raw grayscale images into six image processing pipelines, respectively. 

Use “GrayToColor” modules to transfer invisible 16-bit grayscale images to visible RGB images.

Use “IdentifyPrimaryObjects” modules with advanced settings to identify objects of AF, cell nuclei, epithelial/tumor cells, COX-2, PGE2-EP4, and PIK3CA

## Step 2 Remove the small objects (noise)
Use “MeasureObjectsSizeShape” modules to measure the area and shape features of identified AF, nuclei, tumor cells, and positive biomarker objects.

Use “FilterObjects” modules to remove the small objects (noise) less than 40 pixels (in area value) for three biomarker images and objects less than 20 pixels (in area value) for DAPI and Pan CK images.

The white arrows indicate the small areas removed. Export visible “ObjectsIdentified images” (16-bit RGB TIFF format) in the designated folders for visual quality check.

For the poor-quality images with strong background noise, alternative pipelines with adjusted threshold settings were used for a second or third run to correctly differentiate true signals from background noise. 

## Step 3 Eliminated AF objects
Input the six “ObjectsIdentified” images into an image measurement pipeline for continued image processing.

Use “ConvertImageToObjects” module to convert loaded visible images to calculable objects.

Use “ExpandObjects” module to expand AF objects for 3 pixels for fully removing tissue foldings.

Use “MaskObjects” modules to remove AF objects, tissue folding, and edge effects by overlaying AF images with other fluorophore images to obtain five AF-free images for each sample. The white arrows indicate the eliminated AF objects. 
