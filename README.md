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


Environment files for all used `conda` environments can be found in `conda_envs`. We generally recommend to use [`mamba`](https://github.com/mamba-org/mamba) as dropin replacement for `conda`. 

#### Example for setting up one of the needed environments
```
mamba env create -f path/to/environment.yml
```

#### Virtual environment "anvio"
Setting up `anvio` is a bit more laborious, we followed the instructions provided [here](https://anvio.org/install/).

## 🔍 You want to use the workshop material?!
No problem, you only need to meet a couple of pre-requisites:

* You need access to a system (local or remote) running Linux or MacOS (running Linux makes you a better person, it is good for your karma!🙏).
* You need to set-up `jupyterlab`, including the `bash kernel` mentioned above.
* Set-up the needed `conda environments`, see above.
* Download the mock data.

### Setting up JupyterLab
OK, let's do this. In the following we assume you run a Linux-based system _locally_:

```
### We will set up jupyterlab using mamba
mamba create -n jupyterlab -c conda-forge juypterlab
### We activate the environment and install the bash kernel 
pip install bash_kernel
python -m bash_kernel.install
conda deactivate
### 
```
Once `jupyterlab` is installed, we can run it in the background using `screen`:

```
### Run jupyterlab in the background
screen -S jupyterlab
### New prompt shows up
conda activate jupyterlab
jupyter lab
### jupyterlab should open in your browser!
### you can disconnect from the screen by
### pressing CTRL+A+D
```

Needed `conda` environments can be installed now as described above.

#### Running Jupyterlab on a remote machine
You want to run the material on a remote server? In that case, you set up `jupyterlab` the same way, but on your remote machine. You now need to factor in that your remote machine does not come with a graphical user interface. Therefore, when you connect, you need to actviate port forwarding, so that the output from `juypterlab` is forwarded to your local machine that you use for accessing the remote machine. In the example below we use port `8888`. You can imagine ports as access points that allow communication between machines.

```
### Connect with port forwarding
ssh -L 8888:localhost:8888 user@remote_machine
### Run jupyterlab in the background
screen -S jupyterlab
### New prompt shows up
conda activate jupyterlab
jupyter lab
### You should see text output, your remote
### machine comes usually with no browser.
### Open Jupyterlab locally in your browser:
### http://localhost:8888/lab
### Use the 'token' shown in the text output
### on the remote machine for logging in and
### define a password for future use.
### You are all set now!
### you can disconnect from the screen by
### pressing CTRL+A+D
```

### Download the mock data and the notebooks
The mock data sets (currently only for the first sessions) are availabe from `zenodo`, the `juypter notebooks` are available via this repository.

Download the data/notebooks onto the machine that is running `juypterlab`.

```
### Download the notebooks
git clone https://github.com/wegnerce/chembiosys_metaG_workshop_2023
wget https://zenodo.org/record/8406888/files/chembiosys_metaGWS_mock_data.tar.xz
### unpack the downloaded data from zenodo, and move the two folders into
### chembiosys_metaG_workshop_2023
tar xvf chembiosys_metaGWS_mock_data.tar.xz
mv chembiosys_metaGWS_mock_data/* chembiosys_metaG_workshop_2023
cd chembiosys_metaG_workshop_2023
### check the structure of the folder
tree -L 1 ./
### it should look like this
├── 00_READS
├── 01_QAQC
├── conda_envs
├── LICENSE
├── README.md
└── jupyter_notebooks
```

Please note that some of the used tools require certain DBs:

* [`kaiju`](https://kaiju.binf.ku.dk/server) » we used the 2021 release of refseq [LINK](https://kaiju-idx.s3.eu-central-1.amazonaws.com/2021/kaiju_db_refseq_2021-02-26.tgz) 
* [`checkm`](https://github.com/Ecogenomics/CheckM) » `checkm` was set up for being used with [`metawrap`](https://github.com/bxlab/metaWRAP), we followed these instructions: [LINK](https://github.com/bxlab/metaWRAP/blob/master/installation/database_installation.md) 
* [`gtdbtk`](https://ecogenomics.github.io/GTDBTk/installing/bioconda.html#step-3-download-and-alias-the-gtdb-tk-reference-data) » we used release r207_v2 [LINK](https://data.gtdb.ecogenomic.org/releases/release207/207.0/auxillary_files/gtdbtk_r207_v2_data.tar.gz)

With this you should be all set.

:copyright: Anan Ibrahim, Zander Human, Carl-Eric Wegner 2023

