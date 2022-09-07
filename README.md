#### turbo-memory

# **Understanding Code in Python Notebooks**

##### Predict the relationship between code and comments

### **Description**

The [goal](https://www.kaggle.com/competitions/AI4Code/) is to understand the relationship between code and comments in Python notebooks. We have to reconstruct the order of markdown cells in a given notebook based on the order of the code cells, demonstrating comprehension of which natural language references which code.

### **Context**

Research teams across Google and Alphabet are exploring new ways that machine learning can assist software developers, and want to rally more members of the developer community to help explore this area too. Python notebooks provide a unique learning opportunity, because unlike a lot of standard source code, notebooks often follow narrative format, with comment cells implemented in markdown that explain a programmer's intentions for corresponding code cells. An understanding of the relationships between code and markdown could lend to fresh improvements across many aspects of AI-assisted development, such as the construction of better data filtering and preprocessing pipelines for model training, or automatic assessments of a notebook's readability.

Kaggle has assembled a dataset of approximately 160,000 public Python notebooks from Kaggle and have teamed up with [X, the moonshot factory](https://x.company/) to design a competition that challenges participants to use this dataset of published notebooks to build creative techniques aimed at better understanding the relationship between comment cells and code cells.

### **Data Description**

The dataset(2.16GB) comprises about 160,000 Jupyter notebooks published by the Kaggle community. Jupyter notebooks are the tool of choice for many data scientists for their ability to tell a narrative with both code and natural language. These two types of discourse are contained within cells of the notebook, and we refer to these cells as either code cells or markdown cells (markdown being the text formatting language used by Jupyter).

Our task is to predict the correct ordering of the cells in a given notebook whose markdown cells have been shuffled.

The notebooks in this dataset have been selected and processed to ensure their suitability for the task. All notebooks:
- Have been published publicly on Kaggle under the [Apache 2.0](http://www.apache.org/licenses/LICENSE-2.0) open source license.
- Represent the most recently published version of the notebook.
- Contain at least one code cell and at least one markdown cell.
- Have code written in the Python language.
- Have had empty cells removed.

### **Training Data**

- **train/** - A folder comprising about 140,000 JSON files with the filenames corresponding to the id field in the csv files. Each file contains the code and markdown cells of a Kaggle notebook. The code cells are in their original (correct) order. The markdown cells have been shuffled and placed after the code cells.

- **train_orders.csv** - Gives the correct order of the cells for each notebook in the train/ folder.

    - ```id``` - The notebook in file ```{id}.json```.

    - ```cell_order``` - A space delimited list of the correct cell ordering given in terms of the order in {id}.json.

- **train_ancestors.csv** - On Kaggle, a user may "fork" (that is, copy) the notebook of another user to create their own version. This file contains the forking history of notebooks in the training set. ***Note: There is no corresponding file for the test set.***

    - ```ancestor_id``` - Identifies sets of notebooks that have a common origin or "ancestor". As no notebook in the test set has an ancestor in the training set, you may find this field to be of use as a grouping factor when constructing validation splits.

    - ```parent_id``` - Indicates that some version of the notebook ```id``` was forked from some version of the notebook ```parent_id```. The notebook ```parent_id``` may or may not be present in the training data. (The parent may be missing because someone had forked a private notebook of their own, for instance.)

### **Example Test Data**

To help author submission code, a few example instances selected from the test set have been included. When you submit your notebook for scoring, this example data will be replaced by the actual test data, including the ```sample_submission.csv``` file.

- **test/** - A few example notebooks from the test set. The actual test set comprises about 20,000 notebooks in a format similar to the training set notebooks. No notebook in the test set has an ancestor in the training set.

- **sample_submission.csv** - A sample submission file in the correct format. See the [Evaluation](https://www.kaggle.com/competitions/AI4Code/overview/evaluation) page for more details.

Use [kaggle API](https://github.com/Kaggle/kaggle-api) to access the dataset:
```console
kaggle competitions download -c AI4Code
```
