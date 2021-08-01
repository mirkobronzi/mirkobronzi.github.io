---
title: "Deep Learning Project Template (Cookiecutter)"
tags:
  - coding
  - machine_learning
  - deep_learning
---

## TL;DR
Starting a new Deep Learning (DL) project usually means deciding between a flexible but
less long term-scalable approach(e.g., [Google Colab](https://colab.research.google.com/)),
or a more organized one that requires a decent amount of time/work to set up properly
(in particular when we plan to use several tools that should interact with one-another).

For our new DL projects, we created a [project template](https://github.com/mila-iqia/cookiecutter-pyml)
(Cookiecutter) that can be instantiated in minutes, providing code that runs
out of the box.
The instantiated project contains tools for Deep Learning ([PyTorch](https://pytorch.org/),
[PyTorch Lightning](https://www.pytorchlightning.ai/), [TensorFlow](https://www.tensorflow.org/),
[Keras](https://www.tensorflow.org/api_docs/python/tf/keras)), tools to help running experiments
([MLflow](https://mlflow.org/), [Orion](https://github.com/Epistimio/orion)),
and tools that help with code best practices ([pytest](https://docs.pytest.org/en/6.2.x/),
Continuous Integration, documentation management with [Sphinx](https://www.sphinx-doc.org/en/master/#)).

## What is it

A project template (sometimes called Cookiecutter) is just a template that gets instantiated
(usually providing various options to change the project setup) to bootstrap the project code/environment.
This helps save a lot of time (in particular if the team starts new projects often).

Our [project template](https://github.com/mila-iqia/cookiecutter-pyml) prepare a setup that can be
used for Deep Learning projects. In particular, it provides all the necessary files/folders
that will take care of the boilerplate code necessary to run experiments.
Also, a README file is provided with the final instructions to complete the setup, and with
instructions on how to perform training, running tests, etc.

The goal is to provide all the tools to take care of the research part, and also
all the necessary tools to help the developer to implement best practices (to keep the project
code manageable over time).

### Deep Learning setup

The code is based on either [PyTorch Lightning](https://www.pytorchlightning.ai/) or
[Keras](https://www.tensorflow.org/api_docs/python/tf/keras) (this is a choice left to the developer).
The logging will be performed using MLflow, and a hyper-parameter search can be performed using
[Orion](https://github.com/Epistimio/orion).
The code is already setup to use those libraries.

### Code best practices

A good strategy to help implement best practices is to use automatic checks for code/documentation,
and to write tests to check that the code logic works. It is a good habit to run all those checks
every time that the code is pushed to the server. This can be done by a human, but it is better done
using a continuous integration (CI) process.
To help with this, the instantiated project supports CI tools such as [GitHub actions](https://github.com/features/actions),
Azure and [Travis](https://travis-ci.com/). In fact,
the related configuration files are already provided and ready to run [flake8](https://flake8.pycqa.org/en/latest/)
to check for code format, [Sphinx](https://www.sphinx-doc.org/en/master/#) to check for proper documentation,
and [pytest](https://docs.pytest.org/en/6.2.x/) to run the tests.

## How to use

The [project template](https://github.com/mila-iqia/cookiecutter-pyml) is instantiated with a simple command:

    pip install -U cookiecutter
    cookiecutter https://github.com/mila-iqia/cookiecutter-pyml.git

This command will ask some questions and instantiate the project skeleton.
In particular, it will ask whether the DL backbone should be PyTorch (with PyTorch Lightning) or TensorFlow (with Keras).

After the instantiation is done, the developer will find a working project that can be run
(the README file - in the project itself - will contain the last steps in order to complete the setup,
such as installing the dependencies).
This is because the code includes some synthetic data, a data loader, and a model, all based on a toy task
(i.e., given a sequence of numbers, compute the sum).
Of course, it's the developer's job to change those elements to address their task of interest.

To run the model provided for the toy tasks, it is enough to just:

    cd examples/local
    sh run.sh

Or, if on a cluster that support [Slurm](https://slurm.schedmd.com/sbatch.html), then the command is:

    cd examples/slurm
    sh run.sh

This will train the models (available under `output`), print the log on the screen (or in a file, if using Slurm
) and generate the MLflow plots (under `mlruns`).
More details and instructions are available in the README file contained in the instantiated project itself - enjoy!
