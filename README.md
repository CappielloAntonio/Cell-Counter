# Cell Counter

A python script for tiling large size images and counting object inside them.

## Getting Started

Il lavoro di conteggio delle cellule all'interno del vetrino si divide nelle seguenti fasi:

### Divisione dell'immagine originale in sottoimmagini grandi 1500x1500 pixel

L'immagine viene perlopiù divisa in tile quadrati, ma all'occorrenza vengono salvati anche tile rettangolari di fine immagine.

### Fase di pre processing
- Conversione in scala di grigi dell'immagine analizzata.

- Applicazione del filtro mediano per la riduzione del rumore all'interno dell'immagine. 
  
_The main idea of the median filter is to run through the signal entry by entry, replacing each entry with the median of neighboring entries. The pattern of neighbors is called the "window", which slides, entry by entry, over the entire signal._

- Ricerca dei contorni degli oggetti

- Ricerca delle fontane

### Applicazione dell'algoritmo di segmentazione Watershed

_The watershed is a classical algorithm used for segmentation, that is, for separating different objects in an image._

_Starting from user-defined markers, the watershed algorithm treats pixels values as a local topography (elevation). The algorithm floods
basins from the markers, until basins attributed to different markers meet on watershed lines. In many cases, markers are chosen as local minima of the image, from which basins are flooded._

### Fase di post processing

- Categorizzazione degli oggetti in rilievo

- Conteggio finale
		
I dati estrapolati sono raccolti in forma tabellare in un file CSV contenente il nome del tile e la quantità di oggetti individuati all'interno di esso. Dopo aver ordinato il documento in ordine decrescente di quantità, le 50 immagini contenenti più oggetti vengono salvate in una cartella separata e classificate.

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
