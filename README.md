# ChemBioSys/AquaDiva "Genome-resolved metagenomics workshop" 2023

## ❗Disclaimer
This repository includes the material used for the mentioned workshop and explains how the workshop was prepared (used resources, used tools, ...).

The workshop was organized and given by:
* [Anan Ibrahim](https://github.com/Darcy220606)
* [Zander Human](https://github.com/zander22)
* [Carl-Eric Wegner](https://github.com/wegnerce)

## 💻 Computing resources
For the workshop we used resources provided by [`deNBI`](https://www.denbi.de/cloud) (German Network for Bioinformatics Infrastructure). We had access to:
* 616 cores
* 1.4 TB RAM
* 1 TB of storage

We used these resources (de.NBI large) for creating individual virtual maschines (VM) for every participant:
* 28 VCPUs 
* 64 GB RAM 
* 50 GB root disk

When setting up the VMs we used one of the pre-configured OS images provided by `deNBI`:
* `Jupyterlab-ubuntu22.04 de.NBI (2023-01-10)`

We configured one VM with all needed virtual environments and tools (see below), created a snapshot, and used this snapshot to speed up the set-up of the other VMs.

`deNBI` usually requires users to register using a [`LifeScience RI`](https://lifescience-ri.eu/home.html) account (which is easily done via the particants home institution). The whole procedure is outlined [here](https://cloud.denbi.de/wiki/registration/). However, for workshops, `deNBI` provides the option to make use of so-called _hostel_ accounts, which provide participants with a simple _username_ / _password_ combination for logging in. We made use of this option and provided the participants with the [link](https://signup.aai.lifescience-ri.eu/non/registrar/?vo=lifescience_hostel&targetnew=https%3A%2F%2Flifescience-ri.eu%2Faai%2Fhow-use&targetexisting=https%3A%2F%2Flifescience-ri.eu%2Faai%2Fhow-use&targetextended=https%3A%2F%2Flifescience-ri.eu%2Faai%2Fhow-use) needed for setting up such a hostel account.

## 🔧 Used tools/virtual environments
As described above, we used an `Ubuntu` image that comes with [`juypterlab`](https://jupyter.org/) pre-installed.

We use [`jupyter notebooks` ](https://docs.jupyter.org/en/latest/) as course scripts. `jupyter notebooks` can be best imagined as interactive documents that combine cells of plain text as well as cells of code (in our case rather command-line program calls).

Originally developed for `python`, `jupyter notebooks` are meanwhile flexible and can be used for the execution of code from diverse programming languages. For the workshop, we want ed to use code cells to run commands on our virtual maschines. Therefore we needed to install the [`jupyter bash kernel`](https://pypi.org/project/bash_kernel/). In a nutshell, kernels are engines that allow `jupyter notebooks` to run code of a certain language, here `bash`. The `bash kernel` was installed as follows:

```
pip install bash_kernel
python -m bash_kernel.install
```

Afterwards, code cells containing `bash` can be run from within `jupyter notebooks` opened in `jupyterlab`.

### Virtual environments
The workshop comprises in total X blocks:
* 00 Set-up and basic command-line usage
* 01 Sequence data quality control and quality assessment
* 02 Taxonomic profiling, coverage estimation, metagenome assembly and binning
* 03 Phylogenetics/-genomics and pangenomics
* 04 Functional analysis focussing on biosynthetic gene clusters

For each of the blocks we have prepared one `jupyter notebook`. All the tools needed were available through `virtual environments` managed through [`conda`](https://github.com/conda/conda). 

Used tools:
* ...

Environment files for all used `conda` environments can be found in `conda_envs`. We generally recommend to use [`mamba`](https://github.com/mamba-org/mamba) as dropin replacement for `conda`. 

#### Example for setting up one of the needed environments
```
mamba env create -f path/to/environment.yml
```

#### Virtual environment "anvio"
Setting up `anvio` is a bit more laborious, we followed the instructions provided [here](https://anvio.org/install/).

:copyright: Anan Ibrahim, Zander Human, Carl-Eric Wegner 2023

