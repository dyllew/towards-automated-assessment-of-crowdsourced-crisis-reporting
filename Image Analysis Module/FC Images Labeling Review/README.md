# Create Fukuchiyama City (FC) Image Labeling & Prediction Review Folders
  Use the `make_labeling_review_folders_for_FC_img_data.ipynb` following the instructions below to create folders containing the images regarding different results of the annotation, e.g. images for a task which have complete agreement, complete disagreement, etc. between annotators. Additionally, there are analysis folders created for comparing model predictions against annotation results. This resulting folder structures can be seen in the markdown below.

The `make_labeling_review_folders_for_FC_img_data.ipynb` notebook requires Python version >=3.6 and [pipenv](https://pypi.org/project/pipenv/) installed

From the terminal:
1. Once `pipenv` is installed, run: `pipenv install ipykernel`
2. Activate your virtual environment with `pipenv`, by running `pipenv shell`
3. Create project kernel: `python -m ipykernel install --user --display-name [name-of-your-kernel] --name [name-of-your-kernel]`
5. Launch Jupyter notebook with `jupyter notebook` command and make sure to select the `[name-of-your-kernel]` kernel.

In the Notebook:

6. Set the `SRC_PATH` variable to the directory containing the directories corresponding to the parent directories of the file paths in the `file_path` column in various CSVs.
7. Set the `LABELING_REVIEW_PATH` variable to the directory containing `FC_agreement.csv` and `FC_labels_snapshot.csv`.
8. Set the `FC_PRED_IMAGES_PATH` variable to the directory containing `FC_image_data_preds.csv`. 
9. Run the entire notebook which results in the folder structures shown below useful for reviewing annotation results and predictions.

### **Directory for reviewing annotation**
```
LABELING_REVIEW_PATH # Directory containing folders for each task which contain folders of images which corresponded to different types of agreement between annotators
├── FC_labels_snapshot.csv # CSV containing file paths to images on host machine and every annotator's label given to an image for each task
├── FC_agreement.csv # CSV containing file paths to images on host machine and boolean fields for each type of agreement that can occur on an image, e.g. complete agreement, complete disagreement, plurality but not complete agreement
├── damage_severity 
|   ├── is_complete_agreement # Images for the damage severity task in which all annotators selected the same label, i.e. all agreed
|   ├── is_complete_disagreement # Images in which each annotator selected a different, unique label, i.e. all disagreed
|   └── is_plurality_agreement_and_not_complete_agreement # Images in which there is plurality label, but not complete agreement between annotators
├── humanitarian_categories
├── informativeness                       
├── flood_presence
└── plurality_not_complete_agreement_incorrect_preds
    ├── damage_severity.csv # CSV containing file paths to images on host machine, ground-truth labels, and predicted labels for FC images for the damage severity task
    ├── damage_severity # Images for which there was plurality but not complete agreement between annotators and the prediction was incorrect, i.e. differed from the plurality label
    ├── humanitarian_categories.csv
    ├── humanitarian_categories
    ├── informativeness.csv
    ├── informativeness
    ├── flood_presence.csv                    
    └── flood_presence
```

### **Directory for reviewing predictions against ground-truth**

```
FC_PRED_IMAGES_PATH # Directory containing folders for each task which compare the prediction given to an image against the ground-truth label
├── FC_image_data_preds.csv # CSV containing file paths to images on host machine, ground-truth labels, and predicted labels for FC images
├── damage_severity 
|    ├── correct
|    |   ├── little_or_none  # directory containing images correctly predicted as "little_or_none"
|    |   ├── mild
|    |   └── severe
|    ├── incorrect
|    |   ├── little_or_none # directory containing images incorrectly predicted as "little_or_none"
|    |   ├── mild
|    |   └── severe
|    └── unlabeled  
|        ├── little_or_none # directory containing unlabeled images predicted as "little_or_none"
|        ├── mild
|        └── severe
├── humanitarian_categories
├── informativeness                         
└── flood_presence 
```   

