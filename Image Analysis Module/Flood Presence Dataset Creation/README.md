# Create Flood Presence Train/Dev/Test Splits & Image Folders
  Use the `make_flood_presence_dataset.ipynb` following the instructions below to create the actual train, dev, and test splits and image folders containing the images for this dataset. This resulting folder structure can be seen in the markdown below, i.e. the created `./splits` & `./flood_presence` directories.

The `make_flood_presence_dataset.ipynb` notebook requires Python version >=3.6 and [pipenv](https://pypi.org/project/pipenv/) installed

From the terminal:
1. Once `pipenv` is installed, run: `pipenv install ipykernel`
2. Activate your virtual environment with `pipenv`, by running `pipenv shell`
3. Create project kernel: `python -m ipykernel install --user --display-name [name-of-your-kernel] --name [name-of-your-kernel]`
3. Launch Jupyter notebook with `jupyter notebook` command and make sure to select the `[name-of-your-kernel]` kernel.

In the Notebook:

4. Run the entirety of the `make_flood_presence_dataset.ipynb` notebook to generate the `./splits` folder, which contains the final splits for the flood presence task & the `./flood_presence` folder which contains the train (`./flood_presence/train`), dev (`./flood_presence/dev`), and test (`./flood_presence/test`) splits with a folder structure that can be used by the convenient `ImageFolder` class in PyTorch, namely:
```
.
├── splits                                # Contains final Flood Presence train/dev/test split CSVs which are used to create image folders
├── flood_presence                    # Folder containing split image folders from src_data images, created when all cells of create_image_split_folders.ipynb are run.
│   ├── train
│   │   ├── flood
│   │   └── not_flood
│   ├── dev   
│   │   ├── flood
│   │   └── not_flood           
│   ├── test
│   │   ├── flood
│   │   └── not_flood          
│   └── ...                               # corresponding split CSVs with new image paths corresponding to image folders.
├── src_data                              # Contains source data [1-5] that composes this dataset
└── ...             
```                       
**IMPORTANT NOTE:**

Some of the tweet data we use is produced from rehydrating tweets from tweet IDs. Because of this, **some tweets have been deleted** since the work conducted in the [original work](https://github.com/dyllew/towards-automated-crowdsourced-crisis-reporting) which created the first version of the Flood Presence dataset and Train/Dev/Test splits. If you would like to access to the original tweets used to create the original Flood Presence dataset as was used in the [original work](https://github.com/dyllew/towards-automated-crowdsourced-crisis-reporting), please email [url_googleai@mit.edu](mailto:url_googleai@mit.edu) using subject line **[Flood Presence Dataset]** with your request for the Flood Presence Dataset and your plans for using it. We can only permit use for non-commercial research in accordance with [Twitter's Content Redistribution Policies](https://developer.twitter.com/en/developer-terms/agreement-and-policy) and you must agree to comply with the Twitter Terms of Service, Privacy Policy, Development Agreement, and Developer Policy before receiving the dataset.

By using this dataset you are agreeing to comply with the terms of use of the original data sourcers (namely these [Terms of Use](https://crisisnlp.qcri.org/terms-of-use.html)) and Twitter's Terms of Service, Privacy Policy, Development Agreement, and Developer Policy which can be found [here](https://developer.twitter.com/en/developer-terms/agreement-and-policy).

**Please cite the following sources if you are using this dataset in your research**:

## References
---
[1] ***Firoj Alam, Ferda Ofli, Muhammad Imran, Tanvirul Alam, Umair Qazi, [Deep Learning Benchmarks and Datasets for Social Media Image Classification for Disaster Response](https://arxiv.org/pdf/2011.08916.pdf), In 2020 IEEE/ACM International Conference on Advances in Social Networks Analysis and Mining (ASONAM), 2020.***
```
@inproceedings{crisisdataset2020-images,
Author = {Firoj Alam and Ferda Ofli and Muhammad Imran and Tanvirul Alam and Umair Qazi},
Keywords = {Social Media, Crisis Computing, Tweet Text Classification, Disaster Response},
Title = {Deep Learning Benchmarks and Datasets for Social Media Image Classification for Disaster Response},
Publisher = {IEEE},
Booktitle = {2020 IEEE/ACM International Conference on Advances in Social Networks Analysis and Mining (ASONAM)},
Year = {2020}
}
```

[2] ***Firoj Alam, Ferda Ofli, and Muhammad Imran, CrisisMMD: Multimodal Twitter Datasets from Natural Disasters. In Proceedings of the 12th International AAAI Conference on Web and Social Media (ICWSM), 2018, Stanford, California, USA.***
```
@InProceedings{crisismmd,
  author = {Alam, Firoj and Ofli, Ferda and Imran, Muhammad},
  title = { CrisisMMD: Multimodal Twitter Datasets from Natural Disasters},
  booktitle = {Proceedings of the 12th International AAAI Conference on Web and Social Media (ICWSM)},
  year = {2018},
  month = {June},
  date = {23-28},
  location = {USA}}
```
[3] ***Hussein Mozannar, Yara Rizk, and Mariette Awad, Damage Identification in Social Media Posts using Multimodal Deep Learning, In Proc. of ISCRAM, May 2018, pp. 529–543***
```
 @inproceedings{multimodal-deep-learning, title={Damage Identification in Social Media Posts using Multimodal Deep Learning}, booktitle={ISCRAM 2018 Conference Proceedings – 15th International Conference on Information Systems for Crisis Response and Management}, author={Mouzannar, Hussein and Yara Rizk and Awad, Mariette}, year={2018}, pages={529--543}} 
```

[4] ***Björn Barz, Kai Schröter, Moritz Münch, Bin Yang, Andrea Unger, Doris Dransch, and Joachim Denzler.
"Enhancing Flood Impact Analysis using Interactive Image Retrieval of Social Media Images."
Archives of Data Science, Series A, 5.1, 2019.***
```
@article{flood-impact-in-european-context,
  author    = {Bj{\"{o}}rn Barz and
               Kai Schr{\"{o}}ter and
               Moritz M{\"{u}}nch and
               Bin Yang and
               Andrea Unger and
               Doris Dransch and
               Joachim Denzler},
  title     = {Enhancing Flood Impact Analysis using Interactive Retrieval of Social
               Media Images},
  journal   = {CoRR},
  volume    = {abs/1908.03361},
  year      = {2019},
  url       = {http://arxiv.org/abs/1908.03361},
  eprinttype = {arXiv},
  eprint    = {1908.03361},
  timestamp = {Mon, 19 Aug 2019 13:21:03 +0200},
  biburl    = {https://dblp.org/rec/journals/corr/abs-1908-03361.bib},
  bibsource = {dblp computer science bibliography, https://dblp.org}
}
```

[5] ***Björn Barz, Kai Schröter, Ann-Christin Kra, and Joachim Denzler.
"Finding Relevant Flood Images on Twitter using Content-based Filters."
ICPR 2020 Workshop on Machine Learning Advances Environmental Science.***
```
@article{flood-impact-euro-context-twitter,
  author    = {Bj{\"{o}}rn Barz and
               Kai Schr{\"{o}}ter and
               Ann{-}Christin Kra and
               Joachim Denzler},
  title     = {Finding Relevant Flood Images on Twitter using Content-based Filters},
  journal   = {CoRR},
  volume    = {abs/2011.05756},
  year      = {2020},
  url       = {https://arxiv.org/abs/2011.05756},
  eprinttype = {arXiv},
  eprint    = {2011.05756},
  timestamp = {Thu, 12 Nov 2020 15:14:56 +0100},
  biburl    = {https://dblp.org/rec/journals/corr/abs-2011-05756.bib},
  bibsource = {dblp computer science bibliography, https://dblp.org}
}
```
