Benchmark
=========

For the 2D maps, CMC provides a benchmark to compare the results with. It consists in the codes written to train and test the networks together with their actual weights.

Requisites
----------

- python3
- numpy
- `Pytorch <https://pytorch.org>`_
- `optuna <https://optuna.org>`_

Organization
------------

The folder containing the codes and weights is called ``benchmark``, and is located within the ``2D_maps`` folder. Inside it, there are three folders called ``scripts``, containing the codes used to train and test the networks, ``databases`` with the optuna databases and ``weights``, that has the weights of the networks.

scripts
-------

This folder contains the following codes:

- ``architecture.py``. This script contains different architecture models. 
- ``data.py``. This script process the data to train the networks.
- ``train.py``. This is the code used to train the network. 
- ``test.py``. This is the code used to test the network. 

To train a new model on a given field, or a multifield, follow these steps:

1) Open the code ``train.py`` and set the value of the different parameters in the INPUT section.
2) Run the code: ``python train.py``. Note that when using optuna, several trials can be run in parallel (see the optuna documentation for details).
3) The code will output an optuna database, and will save the losses and weights of each of the considered trials.

To test a model on a given field(s), or a multifield, follow these steps:

1) Open the code ``test.py`` and set the value of the different parameters in the INPUT section.
2) Run the code: ``python test.py``. 
3) The code will generate a file with true value of the parameters, together with the mean and standard deviation of the posterior for each parameter.

This colab shows an example on how to train and test a model using these scripts.
   
databases
---------

We use the optuna software to find the best value of the hyperparameters (learning rate, weight decay...etc) of one particular model. Typically, for each field, we perform 50 trials, where a trial corresponds to the training carried out with one particular choice of the value of the hyperparameters. This folder contains the databases created by optuna with the information about the different trials for the different simulation types.

The generic name of one of these files is ``sim_o3_field_all_steps_500_500_o3.db`` where ``sim`` can be IllustrisTNG, SIMBA, or Nbody, ``field`` is the considered field (can be several fields together). In some cases we smooth out the fields with a Gaussian kernel with width ``width`` (in pixel units). The generic name of these files is ``sim_o3_field_all_steps_500_500_o3_smoothing_width.db``.

These files can be read with optuna package, and two arguments are needed:

- ``study_name``. For all our databases, this variable is set to ``wd_dr_hidden_lr_o3``.
- ``storage``. This should be set to the a sqlite database with the name of the file, e.g. ``sqlite:////home/fvillaescusa/CMC/2D_maps/benchmark/databases/SIMBA_o3_HI_all_steps_500_500_o3.db``

We provide an example on how to read the information of these files in this `colab <https://colab.research.google.com/drive/1ab79y_nIr2JkkgtT_QJhjLTJYNjY9M0B?usp=sharing>`_.


weights
-------

This folder contains the weights of all the models trained. Thus, for each field, there will be at least 50 different files containing the weights of the 50 different trials considered. The generic name of these files is:



We provide an example on how to read these files to test one particular model in this colab.


