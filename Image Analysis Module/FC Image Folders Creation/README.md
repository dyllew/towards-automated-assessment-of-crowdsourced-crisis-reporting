# Create Fukuchiyama City (FC) Image Folders
  Use the `make_image_folders_from_ground_truth_FC_data.ipynb` following the instructions below to create the image folders containing the images from the labeled Fukuchiyama images. This resulting folder structure can be seen in the markdown below, i.e. the `DEST_DIR` directory.

The `make_image_folders_from_ground_truth_FC_data.ipynb` notebook requires Python version >=3.6 and [pipenv](https://pypi.org/project/pipenv/) installed

From the terminal:
1. Once `pipenv` is installed, run: `pipenv install ipykernel`
2. Activate your virtual environment with `pipenv`, by running `pipenv shell`
3. Create project kernel: `python -m ipykernel install --user --display-name [name-of-your-kernel] --name [name-of-your-kernel]`
4. Launch Jupyter notebook with `jupyter notebook` command and make sure to select the `[name-of-your-kernel]` kernel.

In the Notebook:

4. Set the `SRC_DIR` variable to the directory containing the directories corresponding to the parent directories of the file paths in the `file_path` column of `FC_img_data_ground_truth.csv`
5. Set the `DEST_DIR` variable to the directory containing the `FC_img_data_ground_truth.csv`.
6. Run the entire notebook which results in the `damage_severity`, `humanitarian_categories`, `informativeness`, and `flood_presence` image folders in the `DEST_DIR`
```
DEST_DIR
├── FC_img_data_ground_truth.csv # CSV containing file paths to images on host machine and ground-truth (plurality) labels for FC images
├── damage_severity 
├── humanitarian_categories
├── informativeness                         
└── flood_presence 
    ├── flood
    └── not_flood  
```                       

