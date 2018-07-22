# Evaluate KITTI
[![Build Status](https://travis-ci.org/cguindel/eval_kitti.svg?branch=master)](https://travis-ci.org/cguindel/eval_kitti)
[![License: CC BY-NC-SA](https://img.shields.io/badge/License-CC%20BY--NC--SA%203.0-lightgrey.svg)](https://creativecommons.org/licenses/by-nc-sa/3.0/)

The *eval_kitti* software contains tools to evaluate object detection results using the KITTI dataset. The code is based on the [KITTI object development kit](http://www.cvlibs.net/datasets/kitti/eval_object.php) and forked from [eval_kitti](https://github.com/cguindel/eval_kitti).

### Tools ###

* *evaluate_object* is an improved version of the official KITTI evaluation that enables multi-class evaluation and splits of the training set for validation. It's updated according to the modifications introduced in 2017 by the KITTI authors.
* *parser* is meant to provide mAP and mAOS stats from the precision-recall curves obtained with the evaluation script.
* *create_link* is a helper that can be used to create a link to the results obtained with [lsi-faster-rcnn](https://github.com/cguindel/lsi-faster-rcnn).

## Compile the code
in the subfolder 'cpp' of this development kit. It can be compiled via:
```
# In `cpp` folder
mkdir build
cd build
g++ -O3 -DNDEBUG -o evaluate_object ../evaluate_object.cpp
```

or using CMake:

```
mkdir build
cd build
cmake ..
make
```

## After modifying `evaluate_object.cpp`
Everytime after modifying `evaluate_object.cpp`

```
cd build
g++ -O3 -DNDEBUG -o evaluate_object ../evaluate_object.cpp
```
## Directory structure
```
+ eval_kitti
  + cpp
    + build
  + data
    + object
      + label_2 (ground truth labels)
        000000.txt
        000001.txt
        ...
  + results
    + results
      + data
        000000.txt
        000001.txt
        ...
      + plot
        (precision-recall-curve)
      stats_car_detection.txt  
```
## Evaluate

```
# In folder `eval_kitti`
./cpp/build/evaluate_object results
```

## Calculating mAP
```
# In folder `eval_kitti`
python parser.py results
```

## Usage
The `evaluate_object` executable will be then created inside `build`. The following folders are also required to be placed there in order to perform the evaluation:

* `data/object/label_2`, with the KITTI dataset labels.
* `lists`, containing the  `.txt` files with the train/validation splits. These files are expected to contain a list of the used image indices, one per row.
* `results`, in which a subfolder should be created for every test, including a second-level `data` folder with the resulting `.txt` files to be evaluated.

`evaluate_object` should be called with the name of the results folder and the validation split; e.g.: ```./evaluate_object leaderboard valsplit ```

`parser` needs the results folder; e.g.: ```./parser.py leaderboard ```. **Note**: *parser* will only provide results for *Car*, *Pedestrian* and *Cyclist*; modify it (line 8) if you need to evaluate the rest of classes.  

## Copyright
This work is a derivative of [The KITTI Vision Benchmark Suite](http://www.cvlibs.net/datasets/kitti/eval_object.php) by A. Geiger, P. Lenz, C. Stiller and R. Urtasun, used under [CC BY-NC-SA](https://creativecommons.org/licenses/by-nc-sa/3.0/). Consequently, code in this repository is published under the same [Creative Commons Attribution-NonCommercial-ShareAlike 3.0 License](https://creativecommons.org/licenses/by-nc-sa/3.0/). This means that you must attribute the work in the manner specified by the authors, you may not use this work for commercial purposes and if you alter, transform, or build upon this work, you may distribute the resulting work only under the same license.
