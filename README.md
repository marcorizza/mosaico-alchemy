# Mosaico Alchemy

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
[![Python Version](https://img.shields.io/badge/python-3.10%2B-blue)](https://www.python.org/downloads/)
[![Documentation (Mosaico Alchemy)](https://img.shields.io/badge/docs-Mosaico%20Alchemy-blue?logo=readthedocs&logoColor=white)](https://your-project.readthedocs.io)
[![Documentation (Mosaico)](https://img.shields.io/badge/docs-Mosaico-blue?logo=readthedocs&logoColor=white&labelColor=gray)](https://docs.mosaico.dev)

Ingestion pipelines for public robotics datasets into [Mosaico](https://github.com/mosaico-labs/mosaico).

In alchemy, transmutation requires understanding the true nature of what you're working with.
The same applies here: before a dataset can be useful, it needs to be understood, broken down,
and rebuilt into something the platform can actually work with.

That's what this repository does.

## What it is

`mosaico-alchemy` is a collection of ingestion pipelines, called *alchemies*, that take
heterogeneous public datasets (HDF5, TFDS, Parquet, ROS bags) and transmute them into
Mosaico Sequences using the standard SDK ontology.

Pipelines are organized into **packs**, each covering a specific domain. The goal is that
once a dataset is ingested through an alchemy, you can query and stream it the same way you
would any other data in the platform, regardless of where it originally came from.

## Available Packs

| Pack | Datasets | Status |
|:-----|:---------|:-------|
| [Manipulation](src/mosaico_alchemy/manipulation/) | [`reassemble`](https://tuwien-asl.github.io/REASSEMBLE_page/), [`fractal_rt1`](https://research.google/blog/rt-1-robotics-transformer-for-real-world-control-at-scale/), [`droid`](https://huggingface.co/datasets/lerobot/droid_1.0.1), [`mml`](https://zenodo.org/records/6372438) | ✅ Ready |

## Installation

You need a running Mosaico instance. The fastest way to get one is the
[container setup in the docs](https://docs.mosaico.dev/daemon/install/).

Then clone this repo and install with Poetry:

```bash
cd mosaico-alchemy
poetry install
eval $(poetry env activate)
```

Requires Python 3.10+.

## Usage

```bash
# list available alchemies
mosaico-alchemy -h

# run the manipulation alchemy
mosaico-alchemy manipulation \
  --datasets /path/to/reassemble /path/to/droid \
  --host localhost \
  --port 6726 \
  --write-mode sync
```

The CLI is interactive: for each dataset root it will ask which plugin to use,
or let you skip it entirely.

## Extending

New datasets can be added by registering a plugin and the relevant adapters.
The architecture is intentionally open. 

Equivalent exchange applies, you put in the work to describe your data, you get full platform compatibility out.
