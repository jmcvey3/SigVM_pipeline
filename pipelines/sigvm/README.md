# SigVM Ingestion Pipeline

The SigVM ingestion pipeline was created from a cookiecutter template. This README file contains
instructions for running and testing your pipeline.

## Prerequisites

* Ensure that your development environment has been set up according to
[the instructions](../../README.md#development-environment-setup).

> **Windows Users** - Make sure to run your `conda` commands from an Anaconda prompt OR from a WSL shell with miniconda
> installed. If using WSL, see [this tutorial on WSL](https://tsdat.readthedocs.io/en/latest/tutorials/wsl.html) for
> how to set up a WSL environment and attach VS Code to it.

* Make sure to activate the tsdat-pipelines anaconda environment before running any commands:  `conda activate tsdat-pipelines`

## Editing pipeline data fields
This pipeline is set up to handle data created by a Nortek Signature1000 VM running both bottom track and the
echosounder. It also has some basic parameters set up for sampling in Sequim Bay.

1. If you are not running the echosounder, navigate to `pipelines/sigvm/config` and open `retriever.yaml`. 
Remove all entries that have the `_echo` tag. You can do this as well for `dataset.yaml`, but this isn't critical.

2. There are a number of parameters listed in `retriever.yaml` in lines 15-18 that should be updated.

    a. "depth_offset" is the distance below the waterline that the ADCP transducers sit

    b. "salinity" is the water salinity, which is probably around 30 for Sequim Bay inlet, but it varies on the 
    tide.

    c. "magnetic_declination" is the current magnetic declination. You can look this up online.

3. In `dataset.yaml`, update the information under the `attrs` block to something more descriptive for the data 
if desired.

4. There is one parameter listed in `shared/quality.yaml` that can be updated:

    a. "correlation_threshold", on line 71, is for a QC test that removes velocity data below a certain % acoustic signal 
    correlation.


## Running your pipeline
This section shows you how to run the ingest pipeline created by the template.  Note that `{ingest-name}` refers
to the pipeline name you typed into the template prompt, and `{location}` refers to the location you typed into
the template prompt.

1. Make sure to be in the `SigVM_pipeline` folder

2. Run the runner.py with your test data input file as shown below:

```bash
cd $PATH_TO_PIPELINE/SigVM_pipeline
conda activate tsdat-pipelines # <-- you only need to do this the first time you start a terminal shell
python runner.py $PATH_TO_DATA/{filename}.SigVM
```

3. Finally, data and plots are saved in `SigVM_pipeline/storage/root/`
