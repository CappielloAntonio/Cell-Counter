# Cell Counter

A python script for tiling large size images and counting the objects inside them.

## Getting Started

The work of counting the cells inside the slide is divided into the following phases:

### Partition of the source image into subimages of 1500x1500 pixels of width

The image is basically divided into square tiles, but rectangular tiles resulting from the partition can also be saved if necessary.

### Pre processing phase
- Conversion of the image analyzed into greyscale.

- Application of the median filter to reduce the noise within the image. 
  
_The main idea of the median filter is to run through the signal entry by entry, replacing each entry with the median of neighboring entries. The pattern of neighbors is called the "window", which slides, entry by entry, over the entire signal._

Crucial part within the process of finding and counting the cell nuclei. The application of the median filter guarantees that the watershed segmentation algorithm partitions substantial regions of the image (like the nucleus of a cell), disregarding the background noise that might alter the final results.

The image was analyzed three times, applying the median filter twice; no filters were applied the third time. In the latter case we can notice that the segmentation algorithm detected a very high number of nuclei (up to 15 thousand nuclei) even in zones apparently empty, whereas, more in general, it overestimated the number of the cells in the tiles. These results were altered by the background noise of the image that was recognized as an object worth counting. Applying initially the median filter with a 5x5 matrix, then with an 8x8 matrix, we can notice that the value of the nuclei of the recognized cells decreases drastitically and that, in those zones where higher values were obtained, there are only a few cell units, which makes the counting more plausible.

- Research of the objects' outlines

- Research of the fountains

### Application of the Watershed segmentation algorithm

_The watershed is a classical algorithm used for *segmentation*, i.e. for separating different objects in an image._

_Starting from user-defined markers, the watershed algorithm treats pixels values as a local topography (elevation). The algorithm floods basins from the markers, until basins attributed to different markers meet on watershed lines. In many cases, markers are chosen as local minima of the image, from which basins are flooded._

### Post processing phase

- Categorization of the raised objects

- Final counting
		
The extrapolated data are collected in form of a table in a CSV file containing the name of the tile and the quantity of objects identified inside it. After organizing the document according to a decreasing quantity order, the 50 images containing the most objects are saved in a separate folder, then categorized.

## Built With

* [Python 3.7.0](https://www.python.org/) - Programming Language
* [Anaconda](https://www.anaconda.com) - Environment Manager
* [Jupyter Notebook](http://jupyter.org/) - Server-client application that allows editing and running notebook documents via a web browser

## Authors

* [**Antonio Cappiello**](https://github.com/CappielloAntonio) - Initial work

## License

This project is licensed under the MIT License - see the [LICENSE.md](https://github.com/CappielloAntonio/Cell-Counter/blob/master/LICENSE) file for details

## Acknowledgments
* **Stéfan van der Walt** - Scikit-Image founder
* [Scikit-Image General Example](http://scikit-image.org/docs/dev/auto_examples/) - General-purpose and introductory examples for scikit-image
* [Scikit-Image Watershed Segmentation](http://scikit-image.org/docs/dev/auto_examples/segmentation/plot_watershed.html) - The watershed is a classical algorithm used for segmentation, that is, for separating different objects in an image
