# battery-manager-ar-plugin-evaluation

This repo contains the evaluation plots of the new Batterymanager plugin for [Android-Runner](https://github.com/S2-group/android-runner).

## Structure
The [`data`](./data/) folder contains the raw data of the evaluation along with the scripts used to generate the config files for Android-Runner ([experiment generator](./data/experiment_generator.py), [experiment configs](./data/experiments_config.json), and [templates](./data/templates/)), and the [generated config files](./data/GalaxyJ7-W/Experiment0/batch1/config.json) that can be found in `./data/<device>/<experiment>/<batch>/config.json`.

The `out` folder contains the plots of the evaluation.

## How to use
To generate the plots, install the requirements with `pip install -r requirements.txt` and run the [Jupyter Notebook](./analysis.ipynb).

## Note
Due to an error during the experiments, one `.csv` file (`/data/Pixel3-W/Experiment100/batch4/output/2023.07.04_164236/Aggregated_Results_Batterymanager.csv`) was missing in the Pixel3 Experiment 100, batch 4, which is why the [fix_Pixel_experiment.py](./fix_Pixel_experiment.py) file exists. This file fixes the missing `.csv` file by computing it from the other `.csv` files in the same batch. The code is copied from the [Android-Runner implementation](https://github.com/S2-group/android-runner/blob/master/AndroidRunner/Plugins/batterymanager/Batterymanager.py)


# Findings
## General figure descriptions
The vertical axes of the figures show the total energy consumed. The horizontal axis shows the application under test for all figures except for `out/boxplots/experiments_overview_Energy trapz (J).pdf`, where the horizontal axis describes the sample interval for the experiment. Where applicable, the horizontal red dashed line marks the median energy consumed by the **Baseline** application in our runs.

In [this figure](./out/boxplots/all_c_experiment_r_deviceEnergy%20trapz%20(J).pdf) we can see that the median **baseline consumption increases as the sample rate decreases**. This behaviour is explained by the fact that the device needs to do more work because of the high sample rate. This trend occurs relatively consistently throughout the experiments and devices.

In [the same figure](./out/boxplots/all_c_experiment_r_deviceEnergy%20trapz%20(J).pdf) we find a considerable number of outliers. The most dramatic case is in the plot on the last row, fourth column (*NokiaRound-W Experiment 100 Energy trapz (J)*). Here the Local Storage Low Frequency app has a median very close to baseline (around 40J) and a very tight boxplot, whereas the outlier is around 370J.

We also find that the INTERVAL apps (i.e., Cpu INTERVAL, Camera INTERVAL and Display INTERVAL) consume more energy than their regular counterparts. This can be explained by the device needing to use more energy to start and stop the application from running.

One unexpected finding was that the GalaxyJ7 metrics are an order of magnitute smaller than all the other phones. We think it's due to the old Android API (8.0), and, as a result, we decided to adjust the values by multiplying by 1000. 
