# MultipleElectrodeAnalysisANOVA

## Two-Way ANOVA 
### Repeated Measurements


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

