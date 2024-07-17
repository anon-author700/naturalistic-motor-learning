# Naturalistic motor learning dataset

Data can be found at [https://naturalistic-motor-learning.s3.amazonaws.com/data.zip](https://naturalistic-motor-learning.s3.amazonaws.com/data.zip). This data can be loaded using the [croissant](https://github.com/mlcommons/croissant) medata.json file located in this repository. This metadata file returns the filenames for the relevant datafiles and the data needs to be downloaded directly to be accessed. The data is organized into phases, from Phases 1-7, and within each phase there are different data types: control signals, state trajectory signals, contact sensory feedback signals, and mujoco model files. Not all phases contain all types of data.

To access the first state trajectory file of Phase 2, for example, first download and unzip the dataset archive file:

```
wget https://naturalistic-motor-learning.s3.amazonaws.com/data.zip
unzip data.zip
```

Then in Python one could do:

```
import mlcroissant as mlc
import numpy as np

json = "./metadata.json"
ds = mlc.Dataset(jsonld=json)
records = ds.records(record_set='phase-2')
record = next(iter(records))
file_dir = record['phase-2/dir'].decode('UTF-8')
file_name = record['phase-2/filename'].decode('UTF-8')
file_loc = file_dir + '/' + file_name
data = np.load(file_loc)
print(data.shape)
```

Within certain subdirectories of the data directory (each corresponding to a phase of the task) is a helper python file for computing successful target hits and rewards.

A Gymnasium (https://gymnasium.farama.org/) environment called Humanoid2dEnv is available in humanoid2d.py. This can be used to render the simulations.

An example of loading data and rendering the simulation can be found in "example_run.py". Run this with

```
python example_run.py
```
