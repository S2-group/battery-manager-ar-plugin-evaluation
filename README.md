# battery-manager-ar-plugin-evaluation

This repo contains the evaluation plots of the new Batterymanager plugin for [Android-Runner](https://github.com/S2-group/android-runner).

## Structure
The [`data`](./data/) folder contains the raw data of the evaluation along with the scripts used to generate the config files for Android-Runner ([experiment generator](./data/experiment_generator.py), [experiment configs](./data/experiments_config.json), and [templates](./data/templates/)), and the [generated config files](./data/GalaxyJ7-W/Experiment0/batch1/config.json) that can be found in `./data/<device>/<experiment>/<batch>/config.json`.

The `out` folder contains the plots of the evaluation.

## How to use
To generate the plots, install the requirements with `pip install -r requirements.txt` and run the [Jupyter Notebook](./analysis.ipynb).

## Note
Due to an error during the experiments, one `.csv` file (`/data/Pixel3-W/Experiment100/batch4/output/2023.07.04_164236/Aggregated_Results_Batterymanager.csv`) was missing in the Pixel3 Experiment 100, batch 4, which is why the [fix_Pixel_experiment.py](./fix_Pixel_experiment.py) file exists. This file fixes the missing `.csv` file by computing it from the other `.csv` files in the same batch. The code is copied from the [Android-Runner implementation](https://github.com/S2-group/android-runner/blob/master/AndroidRunner/Plugins/batterymanager/Batterymanager.py)
