# Fast Development of Cost Estimates through Machine Learning Algorithms

**Please note: The following repository contains ONLY the README file, documentation and software report attached to the python based library *rapid_cost_estimate*. In the absence of the majority of the original code, much of the functionality of this repository is limited. As such, this repository should serve as an indication as to the scope of the software, and is NOT an indication of the software's quality.**  

**The package was written in conjunction with Wintershall Dea AG, who own the licensing rights to the code. Thus, any individual who would like to make use of this software should contact Wintershall Dea AG.**

## Project description

Many databases are available today that contain historical data on well construction and well cost. These databases make use of statistical analysis to produce P10/P30/P50 cost estimates. However, this statistical analysis often lacks accuracy. The aim of this project is to combine both statistical analysis and machine learning methods to produce higher accuracy cost estimates.

## Installation

The code for this project has been compiled into the package *rapid_cost_estimate*. The instructions to use the package are as follows:

1) Create a python ready environment in your computer
2) Once in the environment, clone the repository using the command:
```sh

$ git clone https://github.com/acse-hst21/Rapid-cost-estimate.git
```
3) Once in the base of the repository, install the package using the command:
```sh

$ pip install -e .
```
Please note, depending on the computational power available, the installation process may take a significant amount of time.

## Usage

First, enter the [config.py](./src/rapid_cost_estimate/config.py) file and set the variable "inflation_index_file" to the appropriate file, depending on the country in which you would like to produce the cost estimate. Note this stage is necessary in order for the inflation model to function correctly.

Then, in the base of the repository, run the following set of commands:

```sh

$ cd scripts
$ python interface.py
```

Having run these commands, the introduction message will be displayed:

![alt text](https://github.com/ese-msc-2021/irp-hst21/blob/62aa80f009eafd5acb03a76ba6d4bc14c5733927/project_images/Introduction.png)

After this, the program will prompt the user to select the number referring to the cost element that they would like to predict for. 

![alt text](https://github.com/ese-msc-2021/irp-hst21/blob/47b240a87e7e90bd2d190bf4887cc5474085437a/project_images/Cost_element_choice.png)

The user is then requested to enter the file containing the input data. This should be a representative set of data for the actual well that the
prediction refers to.

![alt text](https://github.com/ese-msc-2021/irp-hst21/blob/47b240a87e7e90bd2d190bf4887cc5474085437a/project_images/Input_data.png)

After this, the user is presented with a choice. They may either choose to produce the cost element estimation on a pretrained model (all the models available
can be found in the [`saved_models/`](./saved_models) directory) or the user can train a new model.

![alt text](https://github.com/ese-msc-2021/irp-hst21/blob/47b240a87e7e90bd2d190bf4887cc5474085437a/project_images/Choose_model.png)

If the user selects no, they would like to use a pretrained model, the user will be prompted to select which model they would like to choose:

![alt text](https://github.com/ese-msc-2021/irp-hst21/blob/47b240a87e7e90bd2d190bf4887cc5474085437a/project_images/Model_name.png)

The program will then produce the P50 cost estimate for the selected cost element:

![alt text](https://github.com/ese-msc-2021/irp-hst21/blob/47b240a87e7e90bd2d190bf4887cc5474085437a/project_images/Result_old_model.png)

The information regarding the associated error for this estimate can be derived from the model name. Please see the README.md file in the [`saved_models/`](./saved_models) directory for more information.

If the user had previously selected yes, they would like to train a new model then the user will be prompted to re-confirm the cost element they would like to predict for, before being prompted to enter the name for the model they would like to train. 

![alt text](https://github.com/ese-msc-2021/irp-hst21/blob/260779383590e953b2e053af42d2be6cf5f36096/project_images/Name_new_model_updated.png)

The user will then be prompted to enter the path to the dataset that they would like to train the model on. Preferably this would be a different dataset to the input dataset, however, if there is a lack of data then it is acceptable to re-enter the input dataset here.

![alt text](https://github.com/ese-msc-2021/irp-hst21/blob/260779383590e953b2e053af42d2be6cf5f36096/project_images/Train_data.png)

The software will then begin to train the new model. This may take several minutes. Once this process has been completed, the software will produce the P50 cost estimate for the selected cost element, as well as give the associated error for the model:

![alt text](https://github.com/ese-msc-2021/irp-hst21/blob/260779383590e953b2e053af42d2be6cf5f36096/project_images/Result_new_model.png)

It should be noted that throughout the process, where user inputs are taken, each input is first analysed to ensure it is valid. If the input is found to be invalid, the user will be prompted to re-enter the input. This will continue until the software deems the input to be valid.

## Advanced (developer only)

For a full list of the required libraries, as well as the associated version numbers for these libraries, see the [requirements.txt](./requirements.txt) file. To see the metadata for this project, please see the [setup.cfg](./setup.cfg) file. For an overview of the software architecture, please see the image below.

![alt text](https://github.com/acse-hst21/Rapid-cost-estimate/blob/bae62617a70d48a63a8cec1a1dec707e6f14a72c/project_images/Software%20Architecture.png)

### Continuous integration

This repository makes use of continuous integration via GitHub actions. The workflows used to implement these actions can be found in the [`.github/`](./.github) directory. To see if these tests are passing, please see the heading for the repository where the latest commit message is. Alternatively, to see if the workflows written for this software are passing, please see the two badges below:

[![pylint](https://github.com/ese-msc-2021/irp-hst21/actions/workflows/pylint.yml/badge.svg)](https://github.com/ese-msc-2021/irp-hst21/actions/workflows/pylint.yml)

[![tests](https://github.com/ese-msc-2021/irp-hst21/actions/workflows/tests.yml/badge.svg)](https://github.com/ese-msc-2021/irp-hst21/actions/workflows/tests.yml)

### Code documentation

Code is documented in several ways. Code is fully commented throughout the software to allow for easy reader understanding. Each function has an associated docstring attached, which can be seen within the function. Alternatively, Sphinx has been used to auto-generate code documentation. This documentation can be found at [docs/\_build/html/index.html](./docs/_build/html/index.html).
