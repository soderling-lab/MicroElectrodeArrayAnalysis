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

If you would like to do an ANOVA Repeated Measures analysis, set `ANOVARM = True`. From here, if you run all the cells



currdir= os.getcwd()
parent = os.path.dirname(currdir)
gparent=os.path.dirname(parent)
lines_to_skip = 10 # adjust

EXPERIMENT_TIME = "1_MIN"
plate_type = 'DIV19' #adjust

PERTURBATION = "CNO" # adjust
firstTableHeading = "Number of Spikes"
## conditions taken: ### we will define this as dose1,dose2, dose3, dose4, each incrementing in terms of doses

FOLDER_PATH = f"{parent}/data/Div19_CNO/Div19_1minute" #
folder_dict = {}
balances= {"basal": "",
        "dose1": "",
        "dose2": "",
        "dose3": "",
        "dose4": ""
        }

## WALK Through folder of interest
for dirpath, dirnames, filenames in os.walk(FOLDER_PATH):
    if dirpath != FOLDER_PATH:
        folder_dict[dirpath.split("/")[-1]] = dirpath
    elif not dirnames:
        folder_dict['basal'] = dirpath

## get doses names in increasing order 
dose_names = [name for name in folder_dict.keys() if 'basal' not in name]
dose_names.sort(key=custom_sort)

# Initialize balances dictionaryd
balances = {"basal": "basal"}

## map sorted doses
for i, dose_name in enumerate(dose_names, start=1):
    balances[f"dose{i}"] = dose_name.split("_")[-1]

## repeated measures ANOVA test?
ANOVARM = True

print("Balances:", balances)
folder_dict