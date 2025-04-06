<<<<<<< HEAD

This project aims at showcasing some Deep Learning use cases in terms of image
analysis, especially regarding semantic segmentation.


# Content

The project contains the following folders:

+ [deeposlandia](./deeposlandia) contains the main Python modules to train and
  test convolutional neural networks
+ [docs](./docs) contains some markdown files for documentation purpose
+ [examples](./examples) contains some Jupyter notebooks that aim at
  describing data and building basic neural networks
+ [images](./images) contains some example images to illustrate the Mapillary
  dataset as well as some preprocessing analysis results
+ [tests](./tests); `pytest` is used to launch several tests from this folder.

Additionally, running the code may generate extra subdirectories in the chosen
data repository.

# Installation

## Requirements

The code has been run with Python 3. The dependencies are specified in
`setup.py` file, and additional dependencies for developing purpose are listed
in `requirements-dev.txt`.

### From source

```
$ git clone https://github.com/Thevanshgupta/semantic-segmentation-of-WMS-services-fina)
$ cd deeposlandia
$ virtualenv -p /usr/bin/python3 venv
$ source venv/bin/activate
(venv)$ pip install -r requirements-dev.txt
```

### GDAL

As a particular case, GDAL is not included into the `setup.py` file.

For `Ubuntu` distributions, the following operations are needed to install this
program:

```
sudo apt-get install libgdal-dev
sudo apt-get install python3-gdal
```

The `GDAL` version can be verified by:

```
gdal-config --version
```

After that, a simple `pip install GDAL` may be sufficient, however considering
our own experience it is not the case on Ubuntu. One has to retrieve a `GDAL`
for Python that corresponds to the `GDAL` of system:

```
pip install --global-option=build_ext --global-option="-I/usr/include/gdal" GDAL==`gdal-config --version`
python3 -c "import osgeo;print(osgeo.__version__)"
```

For other OS, please visit the `GDAL` installation documentation.

## Running the code

A command-line interface is proposed with 4 available actions (`datagen`,
`train`, `infer` and `postprocess`), callable as follows:

```
deepo [command] --options
```

Some files document the command use:

- [Preprocessed dataset generation](./docs/preprocessing.md)
- [Train a model](./docs/training.md)
- [Infer labels](./docs/inference.md)
- [Postprocess results for geographic datasets](./docs/postprocess.md)
- [Run your own web app instance](./docs/webapp.md)

# Supported datasets

## Mapillary

In this project we use a set of images provided
by [Mapillary](https://www.mapillary.com/), in order to investigate on the
presence of some typical street-scene objects (vehicles, roads,
pedestrians...). Mapillary released this dataset on July 2017, it
is [available on its website](https://www.mapillary.com/dataset/vistas) and may
be downloaded freely for a research purpose.

As inputs, Mapillary provides a bunch of street scene images of various sizes
in a `images` repository, and the same images after filtering process in
`instances` and `labels` repositories.

There are 18000 images in the training set, 2000 images in the validation set,
and 5000 images in the testing set. The testing set is proposed only for a
model test purpose, it does not contain filtered versions of images. The raw
dataset contains 66 labels, splitted into 13 categories. The following figure
depicts a prediction result over the 13-labelled dataset version.

![Example of image, with labels and predictions](https://github.com/Oslandia/deeposlandia/raw/master/images/mapillary_prediction_example.png)

## AerialImage (Inria)

In the [Aerial image dataset](https://project.inria.fr/aerialimagelabeling/files/),
there are only 2 labels, i.e. `building` or `background` and consequently the
model aims at answering one single question for each image pixel: does this
pixel belongs to a building?

The dataset contains 360 images, one half for training one half for
testing. Each of these images are 5000*5000 `tif` images. Amongst the 180
training images, we assigned 15 training images to validation. One example of
this image from this dataset is depicted below.

![Example of image, with labels and predictions](https://github.com/Oslandia/deeposlandia/raw/master/images/aerial_prediction_example.png)

## Shapes

To complete the project, and make the test easier, a randomly-generated shape
model is also available. In this dataset, some simple coloured geometric shapes
are inserted into each picture, on a total random mode. There can be one
rectangle, one circle and/or one triangle per image, or neither of them. Their
location into each image is randomly generated (they just can't be too close to
image borders). The shape and background colors are randomly generated as well.

## How to add a new dataset?

If you want to contribute to the repo by adding a new dataset, please consult the [following instructions](./docs/add_a_dataset.md).

