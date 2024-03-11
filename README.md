# MicroElectrodeArrayAnalysis
Neurons are cell types in the brain that communicate with electrical impulses to send and receive signals to regulate an organism's system. We analyze how these neurons react in vitro to mutations and chemical perturbations using Microelectrode Arrays. Specifically, we use the instrument from Axion Biosystems, which is a small chip with a grid of electrodes to record activity of neurons on the plate. When more than one electrode receives a signal of electrical impulses, it is indicative of multiple neurons firing at the same time. The following table details the different measurements taken from neuronal activity. 

\table here.. ok for public?

MEA data is profound because it captures the symphony of neural activity, demonstrating the brain (brain slice) operating as a network.

Upregulation of certain proteins can cause varying neurotic illnesses. We test whether the knockout of certain genes transcribing these proteins stimulate neuronal activity similar to certain illnesses (ie. epilepsy). We specifically test whether our genes of interest have an effect when knocked out. Additionally, we study whether the introduction of certain chemical dosages have an effect on the neural network. Given these knockouts and varying dosing of the network, we conclude whether the knockout, chemical perturbation, or a combination of the two have an effect on the system.

## Analysis
### Two-Way ANOVA
The effect of two independent variables (IV) on a continuous dependent variable can be studied with Analysis of Variance (ANOVA) tests. Here,  we investigate the influence of gene knockout and chemical perturbation on measurements recorded by Multi-Electrode Array (MEA). This analysis will assess the independent effects of the gene knockout and chemical perturbation, as well as their combined impact on neuronal networks in vitro. Our hypothesis posits that the neuronal response to chemical perturbations may differ significantly between a control system and one with a gene knockout.

#### Repeated Measurements
Since we analyze ~24-36 replicates at a time (2-3 MEA plates) and have six mutant conditions, we must perform a Repeated Measures (RM) 2-way ANOVA test to adjust for variances within the same experiment.  When there are changes in the mean across $\geq 3$ time points OR the same subjects (knockout genes) have varying means across $\geq 3$ or more conditions, repeated measurement corrections should be used[[1]](##References). 

_MANOVA? Multivariate Analysis: When there are multiple dependent variables, you might consider a multivariate approach like MANOVA (Multivariate Analysis of Variance). MANOVA is used to test hypotheses about the effects of independent variables on multiple dependent variables. It's like ANOVA, but for multiple correlated dependent variables._


### T-tests
We compare the neural activity of a system with a specific gene (gene G) knocked out to that of a controlled, normally functioning system. This comparison is made regardless of chemical dosing. We hypothesize knocking out gene G will result in changes in neural activity. The extent of these changes depends on the specific test parameter being measured. For instance, we might expect the Mean Firing Rate (Hz) to increase, while the Percent Bursts with Start Electrode could decrease.

To analyze these differences, we perform t-tests between the two groups (knockout vs. control) across multiple test parameters, all derived from the same sample. To account for the risk of Type I errors (false positives) inherent in conducting multiple tests, we adjust for multiple testing using the Bonferroni method. This method conservatively adjusts the alpha value (our significance threshold) to reflect the number of tests being conducted. Normally, a significance value of $\leq 0.05$ is considered indicative of a significant difference between the two groups. However, with the Bonferroni adjustment, this threshold is modified on a case-by-case basis, depending on the number of parameters measured.

#### Plot
We visualize the t-test results across chemical dosings using a line graph plotting fold change (mutant / control). This approach illustrates the extent of change in the knockout system compared to the control (unt2). When the p-value is found to be significant after adjusting for multiple testing, we highlight the corresponding fold-change on the graph with a red outline. You can access the detailed procedure for this analysis in our pipeline, available at:  [plot_ttest.ipynb](analysis/plot_ttest.ipynb)

![CNO treatment on Div19 across varying dosages T-test results](https://github.com/soderling-lab/MultipleElectrodeArrayAnalysis/blob/clean/t-test_results/Div19_CNO/Div19_1minute/plots/Mean%20Firing%20Rate%20(Hz).png)
### Bar plots (comparison)
To visualize the effect of each knockout and chemical dosages, we plot a bar chart to demonstrate the trend for each knockout/control and the effect of the different chemical concentrations on each gene of interest.

![CNO treatment on Div19 monitored for 1min](https://github.com/soderling-lab/MultipleElectrodeAnalysisANOVA/blob/clean/bar_charts/CNO/DIV19/1_MIN/Mean%20Firing%20Rate%20(Hz).png)

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


### T-Test 
To perform a t-test with neuronal data between a __gRNA perturbation___ and control system, please navigate into [t-test.ipynb](analysis/t-test.ipynb) and adjust the data as indicated (#adjust) and run the remaining cells. The t-test results will be saved under [t-tests_results/](t-test_results) as both `.csv` files and a singular `.xlsx`. If you are dealing with a number of different doses, it will create a worksheet for each dose, showing variation between mutant gRNA and control (unt2). The t-statistic and p-value are provided as results.

## References
[1] Repeated measures anova. Repeated Measures ANOVA - Understanding a Repeated Measures ANOVA | Laerd Statistics. (n.d.). https://statistics.laerd.com/statistical-guides/repeated-measures-anova-statistical-guide.php 
