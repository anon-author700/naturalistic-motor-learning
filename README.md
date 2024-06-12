# Naturalistic motor learning dataset

Data can be found at [https://naturalistic-motor-learning.s3.amazonaws.com/data.zip](https://naturalistic-motor-learning.s3.amazonaws.com/data.zip). This data can be loaded using the [croissant](https://github.com/mlcommons/croissant) medata.json file located in this repository. This metadata file returns the filenames for the relevant datafiles, so the data needs to be downloaded directly to be accessed. The data is organized into phases, from Phases 1-7, and within each phase there are different datatypes of control signals, state trajectory signals, contact sensory feedback signals, and mujoco model files. Not all phases contain all types of data.

To access the first state trajectory file of Phase 2, first download and unzip the dataset archive file:

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
records = ds.records(record_set='phase-2/state')
record = next(iter(records))
file_loc = record['phase-2/state-path'].decode('UTF-8')
states = np.load(file_loc)
print(states.shape)
```
