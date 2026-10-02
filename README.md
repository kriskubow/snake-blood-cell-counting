# Snake Blood Cell Counting
This repository contains code for counting cells in snake blood smears (Giemsa stain) that was used in a manuscript that is currently in review (details to be updated upon acceptance). The ImageJ macro (bloodCellCounting2.ijm) implements an ilastik pixel classification model (bloodSegmentation3.ilp) to identify and count the cells in a given image. 

## Dependencies
Running the ImageJ macro requires the [FIJI](https://fiji.sc/) version of ImageJ and that you install the [MorphoLibJ plugins](https://github.com/ijpb/MorphoLibJ) and [ilastik plugin](https://www.ilastik.org/documentation/fiji_export/plugin#installation). You must also have installed [ilastik](https://www.ilastik.org/) and then [set the executable path in the ImageJ](https://github.com/ilastik/ilastik4ij#configuration-for-running-ilastik-from-within-Fiji) so that it can find the application.

## Running the analysis
You only need to download the ImageJ macro and ilastik files. Run the analysis by opening and running the macro in ImageJ. It will ask you to select the location of the ilastik model file and the image you want to analyze. You do not open the ilastik file; it's accessed directly by the macro. The macro will perform a white-balance correction based on a manually selected background region. 

## About the ilastik pixel classification model
Eleven images spanning a diversity of conditions and sample qualities were used to train the pixel classifier in ilastik. Because erythrocytes and leukocytes are both nucleated cells in snakes, three classifications were used: erythrocyte nuclei and leukocytes, erythrocyte cytoplasm, and background. Erythrocytes were ultimately identified by their nuclei to avoid segmentation complications due to overlapping cell bodies whereas nuclei rarely overlapped. The training images are provided as examples (folder: white balance training set), but they are not required to run the macro. 

Note that the classifier was trained for this specific dataset and may not work as well on your images, depending on how much they differ. If you are getting sub-optimal results, we recommend that you train your own pixel classifier using your specific data rather than attempt to modify our model. Indeed, because ilastik is picky about file paths, it may not even be possible for you to open our model file in ilastik. Creating your own pixel classification model is not too difficult - see [this tutorial](https://www.ilastik.org/documentation/pixelclassification/pixelclassification). There are also many other good resources online.

## Limitations
The macro will count all cells, but may exclude some leukocytes. Manually inspecting the results is recommended.
