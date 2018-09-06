# Reinforcement Learning For Games

## Install Instructions

### Singularity

The way used throughout the project was via Singularity.

*   Install Singularity - https://singularity.lbl.gov/install-linux
    *   This must be done on a personal machine! Singularity needs `root`
        access for the initial build.
*   Swap to the repo folder.
*   Run `sudo singularity build starcraft.simg Singularity`.
    *   This is going to install everything, so takes a while.
*   Can be used either with:
    *   `singularity shell -C starcraft.simg`
    *   `singularity exec starcraft.simg python run.py ${SCRIPT_ARGS}`
    *   If running on a machine that has a GPU + CUDA, ensure to pass `--nv`
        after `shell` or `exec`.

### Poetry

Only used initially, so may not be fully working.

* Install SC2. If installed to a non-standard location set the `$SC2PATH`
 environment variable to point to the install location.
    * An example of the install and setting this variable is in the
     `Singularity` install file.
* Install [poetry](https://github.com/sdispater/poetry) with `pip install poetry`.
* Once installed, use `poetry install`. This will create a virtualenv and
 install all needed packages into it.
* Then you can call the scripts like so:
```sh
poetry run python CNN/run.py --map_name MAP_NAME --model_name MODEL_NAME --training=False
```

## Instructions to Run

An example script of running the CNN can be found in `CNN\runPySC2.sh`, which
uses Singularity. The paths in this script will need updating for a different
user.

To run a specific pretrained CNN model, the script should be called as follows,
where `MAP_NAME` is the map or mini-game in question and `MODEL_NAME` is the
exact name of the model, as stored in `CNN\_files\`.

```sh
python run.py --map_name MAP_NAME --model_name MODEL_NAME --training=False
```

The folders for the models should look as follows:

```
CNN/_files/
├── models
│   └── test_model_20
│       ├── checkpoint
│       ├── model.ckpt-13000.data-00000-of-00001
│       ├── model.ckpt-13000.index
│       ├── model.ckpt-13000.meta
│       ├── model.ckpt-13500.data-00000-of-00001
│       ├── model.ckpt-13500.index
│       └── model.ckpt-13500.meta
└── summaries
    └── test_model_20
        └── events.out.tfevents.1521839337.db12gpu1.arc3.leeds.ac.uk
```

To train a new model, instead drop the `--training=False`. It is necessary to
add `--if_output_exists=continue` to continue training an already existing model.
The full set of runtime flags can be found in [run.py](CNN/run.py)
