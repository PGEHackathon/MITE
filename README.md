<a href="https://www.pge.utexas.edu">
  <img src="https://github.com/PGEHackathon/mite/blob/main/pge_logo.png" alt="Alt text" width="400"/>
</a>

# Energy A.I. High School Hackathon 2025, First Annual Hackathon 

## Hackathon Hosts: [Prof. Michael Pyrcz](https://twitter.com/GeostatsGuy) and [Prof. John Foster](https://twitter.com/johntfoster)

#### Background

We challenge the Energy A.I. hackathon teams, visiting The University of Texas at Austin, to build a data science model to predict oil production. This will require:

* data analysis and evaluation of multiple data sources and a variety of features
* training and tuning robust machine learning prediction models

This data-driven approach will replace the conventional engineering and geoscience approach:

* characterizing and modeling the subsurface
* physics-based fluid flow simulations

#### Technology Opportunity

Current engineering and geoscience numerical simulation methods to forecast oil production are extemely expensive,

* professional time to build and interpret the models

* computational time to run the numerical simulations

This cost limits the exploration of the subsurface. With fast data science-based machine learning prediction models we can,

* improve the exploration of subsurface uncertainty and risk to reduce environmental impacts

* improve optimization of development decision making to maximize profit while reducing environmental impacts

___
 
#### The Reservoir Unit, Known as 'Reservoir 21'

Reservoir 21 is a large, isolated reservoir unit with good porosity and permeability. The reservoir rock was deposited by submarine turbidity currents that transported sand, sand-shale, and shale to the deep ocean basin. Later on the pore space was filled by migrating hydrocarbons that were trapped by a thick shale above the unit. 

<a href="https://en.wikipedia.org/wiki/Turbidite#/media/File:Turbidite_formation.jpg">
  <img src="/resources/Turbidite_formation.jpg" alt="Alt text" width="400"/>
</a>

**Figure 1:** Turbidite formation showing sediment deposition patterns in underwater environments (image from Wikipedia Article, Turbidite).


Specifications of the reservoir unit of interest: 

* **Depositional Setting**: clastic deepwater reservoir unit with extents 10km by 10km by 50m (thickness)
* **Fluids**: initial oil water contact is at the depth of 3067.4m and the average connate water saturation is about 20.3%
* **Structure**: Anticline structure with a major vertical fault that crosses the reservoir (see location and equation on the image below). 
* **Grids**: the 2D maps conform to the standard Python convention, origin on Top Left (see the image below).

<img src="https://github.com/PGEHackathon/mite/blob/main/problem/res21_planview.png" width="600" height="400">

**Figure 2:** Planview of Reservoir 21.

* **Wells**: 83 vertical wells were drilled across the reservoir and completed throughout the payzones. Due to the field management cosntraints, only 73 wells were open to produce oil for the first three years, while the remaining 10 wells were kept shut-in. At the end of the third year, the remaining 10 unproduced wells are planned to be openned.

* **Question**: What will be the the cumulative oil production for each of these 10 unproduced (preproduction) wells over the next 3 years?  

___

### Available Data Files Inventory

You have the following data files available.

#### Well Logs

These two files contain the well log data along the wellbore for all 83 wells.

* [**res21_2D_wells.csv**](/problem/res21_2D_wells.csv) - 2D averaged well data and 3 year cumulative oil production for the previous production wells, well indices from 1 to 73
* [**res21_2D_wells_test.csv**](/problem/res21_2D_wells_test.csv) - 2D averaged well data for the remaining, preproduction wells, well indices from 74 to 83 

Comments: 

* all the well names are masked (replaced with simple indices from 1 to 83) and coordinates transformed to the area of interest to conceal the actual reservoir. 
* available petrophysical and geo-mechanical properties are listed. 
* blank entries in the file indicate missing data at those locations.

Predictor features:

| Feature           | Units                  | Description                                                                 |
|-------------------|------------------------|-----------------------------------------------------------------------------|
| Well ID           | Integer                | Unique well indentifier, anonymized, random integer                         |                                     
| X, Y              | m                      | Well location in area of interest (0 - 10,000 in X and Y)                   |
| Porosity          | %                      | Measure of the void spaces in a material, expressed as a percentage.        |
| Permeability      | mDarcy                 | Ability of a material to allow fluids to pass through its pore spaces.      |
| Acoustic Impedance| $kg/m²·s x 10^6$       | Product of a material's density and sound velocity, affecting wave behavior.|
| Rock Density      | $g/cm^3$               | Mass of a rock per unit volume.                                             |
| P-wave Velocity   | m/s                    | Speed of compressional seismic waves through a material.                    |
| S-wave Velocity   | m/s                    | Speed of shear seismic waves through a material.                            |
| Young's Modulus   | GPa (gigapascals)      | Ratio of stress to strain in the elastic region; measures stiffness.        |
| Shear Modulus     | GPa (gigapascals)      | Ratio of shear stress to shear strain; measures resistance to shear.        |

Response Feature:

| Feature           | Units                  | Description                                                                 |
|-------------------|------------------------|-----------------------------------------------------------------------------|
| Cumul. Oil        | Mbbls                  | Total oil produced by the well over three years in 1000s of barrels         | 

#### Map Data

The following map data are available:

* [**res21_ai_map.npy**](/problem/res21_ai_map.npy) - acoustic impedance (AI) inverted from geophysical amplitudes and interpretations. Hint: high AI indicates less oil
* [**res21_2d_sand_prop_map.npy**](/problem/res21_2d_sand_prop_map.npy) - proportion of sand facies over the vertical column, 2D sand proportion map. Hint: high proportion of sand generally results in more production.

Comments:

* 2D maps are regular grids 200 by 200 cells, cell extents are 50m by 50m, extending over the reservoir 
* values indicate the vertically averaged property, vertical resolution is the entire reservoir unit
* the indices follow standard Python convention, original is top left corner, indices are from 0, 1, ..., n-1 and the first index is the row (from the top) and the second index is the column from the left.
* e.g. to select the 5th grid cell in x (column) and the 10th grid cell in y (rows), use ndarray[9,4] in Python (aside, array[10,5] in Matlab). 
* the origin of the 2D data (e.g., array[0,0]) is the center of the top left cell, 25m and 25m along y and x direction (refer to the image above)

### Required Hackathon Submissions

By Wednesday June 25th at 9:30 pm each team must submit:

* **Solution Table** - a .csv file with your predictions for the 10 preproduction wells. The submitted file should follow the format of the provided template [solution.csv](https://github.com/PGEHackathon/mite/blob/main/resources/solution.csv) for automatic scoring.

    * the file must be named 'solution.csv' with final values in a commit and then pushed to Github for the automated scoring.

* **Python Workflow and Associated Files** - commited to this repository with the workflow as a Jupyter Notebook .ipynb file along with all data files required to reproduce your team's solutions. The submitted workflow Jupyter Notebook should follow the format of the provided template [Hackathon_ProjectTemplate](https://github.com/PGEHackathon/mite/blob/main/resources/Hackathon_ProjectTemplate.ipynb) for enhanced workflow communication and code readibility.

* **Presentation** - a PowerPoint slide deck .PPTX file for your team's final presentation to our judges. The submitted presentation should follow the format of the provided example presentation [Hackathon_PresentationTemplate](https://github.com/PGEHackathon/mite/blob/main/resources/Hackathon_PresentationTemplate.pptx).

The Workflow and Presentation submission templates are in the [resources respository](https://github.com/PGEHackathon/resources) and the results submission template is in this repository.

#### Hackathon Schedule

| Day   | Time                  | Topic                                  | Objective                                                                                      |  Notes  | Demo | Interactive | Video |
|-----------|---------------------------|----------------------------------------|------------------------------------------------------------------------------------------------|------|----|------|------|
| Sunday Day 1 | 7:30 PM - 9:30 PM | Welcome, Introduction                        | introduction / overview, energy data science, machine learning basics, set up – github and codespace  | [e-book](https://geostatsguy.github.io/MachineLearningDemos_Book/MachineLearning_concepts.html) <br> [Introductions](/resources/2025_PGE_HS_Hackathon_Introduction.pdf) <br> [ML Basics](/Pyrcz_Lectures/06_Machine_Learning.pdf)| | [Overfit](/interactive/Interactive_Overfit.ipynb) <br> [Tree Pruning](/interactive/Interactive_Decision_Tree.ipynb) | [VS Code](https://youtu.be/1_VefXlsdgA?si=WbIqOCO2kFd9J6SE) <br> [git and Github](https://youtu.be/0xrsyxsI31A?si=OD3tLFoYmzGH_jQV) <br> [Jupyter Notebooks](https://youtu.be/jSNs4I4abKg?si=OCM5J-uh9fJGIhFd) <br> [Machine Learning](https://youtu.be/zOUM_AnI1DQ?si=2zpu43G_PLGn2ttB) |
| Monday Day 2 | 8:30 AM - 10:30 AM | Data Science in Python | Python packages NumPy, SciPy, matplotlib, etc. |  | | [Correlation](/interactive/Interactive_Correlation_Coefficient.ipynb) <br> [Correlation Issues](/interactive/Interactive_Correlation_Coefficient_Issues.ipynb) |  |
|       | 6:30 PM - 9:30 PM    | Feature Engineering / Feature Imputation | feature imputation, missing data hands on and slides, scikit-learn | [e-book](https://geostatsguy.github.io/MachineLearningDemos_Book/MachineLearning_feature_imputation.html) <br> [Imputation](/Pyrcz_Lectures/05d_Feature_Imputation.pdf) | [Imputation](/Pyrcz_ebook/MachineLearning_feature_imputation.ipynb) | | |
| Tuesday Day 3 | 8:30 AM - 10:30 PM | Feature Engineering / Feature Selection | feature engineering, curse of dimensionality and feature ranking  | [e-book](https://geostatsguy.github.io/MachineLearningDemos_Book/MachineLearning_feature_ranking.html) <br> [Feature Selection](/Pyrcz_Lectures/05b_Feature_Selection.pdf) | [Feature Ranking](/Pyrcz_ebook/MachineLearning_feature_ranking.ipynb)| | [Feature Selection](https://youtu.be/5Q0gemu-h3Q?si=PhgGEQ03QNqXgCFM) |
|       |  2:45 PM - 5:00 PM | Inferential Machine Learning / Cluster Analysis | inferential machine learning, clustering, K-means clustering | [e-book](https://geostatsguy.github.io/MachineLearningDemos_Book/MachineLearning_clustering.html) [Clustering](/Pyrcz_Lectures/07_Clustering.pdf) | [Clustering](/Pyrcz_ebook/MachineLearning_clustering.ipynb) | [Clustering](/interactive/Interactive_kMeans_Clustering.ipynb) | [Clustering](https://youtu.be/oFE10cLl0Fs?si=8Uruksc4mf2djLEd) |
|       | 6:30 PM - 9:30 PM    | Inferential Machine Learning / Dimensionality Reduction | inferential machine learning, dimensionality reduction, PCA  | [e-book](https://geostatsguy.github.io/MachineLearningDemos_Book/MachineLearning_PCA.html) <br> [PCA](/Pyrcz_Lectures/08_DimensionalityReduction.pdf) | [PCA](/Pyrcz_ebook/MachineLearning_PCA.ipynb) | [PCA](/interactive/Interactive_PCA_Rotation.ipynb) | [PCA](https://youtu.be/-to3JXiae9Y?si=YdCk5gwsEQupBoRe) |
| Wednesday Day 4 | 8:30 AM - 9:45 AM     | Predictive Machine Learning | multilinear regression, tree-based methods, decision tree, random forest  | [e-book](https://geostatsguy.github.io/MachineLearningDemos_Book/MachineLearning_linear_regression.html) <br> [Linear](https://github.com/PGEHackathon/mite/blob/main/Pyrcz_Lectures/09_LinearRegression.pdf) <br> [Tree](https://github.com/PGEHackathon/mite/blob/main/Pyrcz_Lectures/14_DecisionTree.pdf) <br> [Forest](https://github.com/PGEHackathon/mite/blob/main/Pyrcz_Lectures/15_EnsembleTree.pdf) | [Linear](/Pyrcz_ebook/MachineLearning_linear_regression.ipynb) <br> [tree](/Pyrcz_ebook/MachineLearning_decision_tree.ipynb) <br> [Forest](/Pyrcz_ebook/MachineLearning_ensemble_trees.ipynb) | [Linear](/interactive/Interactive_Linear_Regression.ipynb) <br> [Tree](/interactive/Interactive_Decision_Tree.ipynb) | [ML Prediction](https://youtu.be/EbYePnjWB5o?si=kv7f3Hwlc_Ov4wSP) <br> [Linear](https://youtu.be/0fzbyhWiP84?si=vItW_WPVc9xC1RUE) <br> [Tree](https://youtu.be/JUGo1Pu3QT4?si=vx54_z0_01ufRfqu) <br> [Forest](https://youtu.be/m5_wk310fho?si=2wIdizheGrnpibxp) |
|       | 6:30 PM - 9:30 PM     | Complete Presentations and Submission         | PowerPoint and Jupyter Notebooks  | [PowerPoint Template](/resources/Hackathon_PresentationTemplate.pptx) [Notebook Template](/resources/Hackathon_ProjectTemplate.ipynb) |  |  | |
| Thursday Day 5  | 8:30 AM - 10:30 AM     | Final Presentations and Awards   |         |  |  |  | |

