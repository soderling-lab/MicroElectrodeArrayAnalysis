# MultipleElectrodeAnalysisANOVA
Neurons are cell types in the brain that communicate with electrical impulses to send and receive signals to regulate an organism's system. We analyze how these neurons react in vitro to mutations and chemical perturbations using Multiple Electrode Arrays. Specifically, we use the instrument from Axion Biosystems, which is a small chip with a grid of electrodes to record activity of neurons on the plate. When more than one electrode receives a signal of electrical impulses, it can be gathered multiple neurons are firing on the plate. The following table details the different measurements taken from neuronal activity. 

\table here 

MEA data is profound because it captures the symphony of neural activity, demonstrating the brain (brain slice) operating as a network. 

Neurons are affected by gRNA mutations 
## Analysis
### Two-Way ANOVA


#### Repeated Measurements


### T-tests

### Plot


## Environment
Please build the environment running `conda env create -f environment.yaml` and push to jupyter-notebook kernel using `python -m ipykernel install --user --name <anovaenv> --display-name "<displayname>"`

## Program Instructions
Navigate into [analysis/](/analysis) and push anovaenv to the python kernel. In the third cell (starting with dir and file assignments), please adjust the number of lines to skip in the MEA data file including the table of the first heading. In order for each mini-table to be processed appropriately, the first table heading is skipped, so you must adjust the `firstTableHeading` parameter to the appropriate heading. Please adjust everything that has the comment `#adjust` beside it. 

### For ANOVA analysis
[2wayANOVA.ipynb](analysis/2wayANOVA.ipynb) 
Data for a singular run should be placed together, such that stepping down from the indicated `FOLDER_PATH` (ie. [/example_data/Div19_CNO/Div19_1minute](example_data/Div19_CNO/Div19_1minute)) will yield the different doses administered (as folders), and plate data is provided as `.csv` files within the dosage folders. If you are dealing with less than 4 extra doses, please take away the extra dose counts defined in balances. 

If you would like to do an ANOVA Repeated Measures analysis, set `ANOVARM = True`. After making the necessary changes in the third cell, you may just run all the cells below with no changes. Please monitor the printed output to ensure the correct data you are looking at is being analyzed. Your data will be saved to the filepathway defined under `SAVE_ANOVA_TABLE_FILE`.

**If you would only like to compare control against a singular dosage: Run [2wayANOVA_2doses.ipynb](analysis/2wayANOVA_2doses.ipynb) with the above adjustments** The default picks the maximum dosage, if you would like to change that, please go in and change it in cell 4. 

### Plot
In order to plot each neuronal measurement (Mean Firing Rate, Area under Cross-Correlation) across all gRNAs and doses, pleas run [plot.ipynb](analysis/plot.ipynb) with the changes indicated under Program Instructions. In the third cell make the necessary changes and ensure the kernel is on anovaenv. The plots for each measurement will be visible and will be saved under (`save_figfile`) the defined pathway [/bar_charts/{PERTURBATION}/{plate_type}/{EXPERIMENT_TIME}/{testparameter}](bar_charts). 

![CNO treatment on Div19 monitored for 1min](https://github.com/soderling-lab/MultipleElectrodeAnalysisANOVA/blob/clean/bar_charts/CNO/DIV19/1_MIN/Mean%20Firing%20Rate%20(Hz).png)

### T-Test 
To perform a t-test with neuronal data between a __gRNA perturbation___ and control system, please navigate into [t-test.ipynb](analysis/t-test.ipynb) and adjust the data as indicated (#adjust) and run the remaining cells. The t-test results will be saved under [t-tests_results/](t-test_results) as both `.csv` files and a singular `.xlsx`. If you are dealing with a number of different doses, it will create a worksheet for each dose, showing variation between mutant gRNA and control (unt2). The t-statistic and p-value are provided as results.

how are neuronrs analyzed with multipleelectode array. i need to introudce neurons, electrochemical analysis... we use brain slices w the MEA and then it gives a bunch of parameters like Mean Firing rate, Area under cross-correlation, number of spikes within burst, etc.