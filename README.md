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

___
 
#### The Reservoir Unit

Specifications of the reservoir unit of interest: 

* **Depositional Setting**: clastic deepwater reservoir unit with extents 10km by 10km by 50m (thickness)
* **Fluids**: initial oil water contact is at the depth of 3067.4m and the average connate water saturation is about 20.3%
* **Structure**: Anticline structure with a major vertical fault that crosses the reservoir (see location and equation on the image below). 
* **Grids**: the 2D maps conform to the standard Python convention, origin on Top Left (see the image below).

<img src="https://github.com/PGEHackathon/mite/blob/main/problem/res21_planview.png" width="600" height="400">

* **Wells**: 83 vertical wells were drilled across the reservoir and completed throughout the payzones. Due to the field management cosntraints, only 73 wells were open to produce oil for the first three years, while the remaining 10 wells were kept shut-in. At the end of the third year, the remaining 10 unproduced wells are planned to be openned.

* **Question**: What will be the the cumulative oil production for each of these 10 unproduced (preproduction) wells over the next 3 years?  

___

### Available Data Files Inventory

You have the following data files available.

#### Well Logs

These two files contain the well log data along the wellbore for all 83 wells.

* **res21_2D_wells.csv** - 2D averaged well data and 3 year cumulative oil production for the previous production wells, well indices from 1 to 73
* **res21_2D_wells_test.csv** - 2D averaged well data for the remaining, preproduction wells, well indices from 74 to 83 

Comments: 

* all the well names are masked (replaced with simple indices from 1 to 83) and coordinates transformed to the area of interest to conceal the actual reservoir. 
* available petrophysical and geo-mechanical properties are listed. 
* blank entries in the file indicate missing data at those locations.

Predictor features:

* well (ID) - is the unique well index
* X (m), Y (m) - are the location coordinates over a square area of interest of 0 - 10,000m in X and Y.
* Porosity (%) - is the measure of the void spaces (pores) in a material, expressed as a percentage of the total rock volume.
* Permeability (mD) - is the ability of a material to allow fluids to pass through it, typically measured by how easily the fluid flows through its pore spaces.
* Acoustic Impedance (kg/m2s*10^6) - is the product of a material's density and the velocity of sound through it, determining how much sound is reflected or transmitted at boundaries between different materials.
* Density (g/cm^3) - is the mass of a rock per unit volume
* P-wave / compressible velocity (m/s) - is the speed at which primary (compressional) seismic waves travel through a material, influenced by the material's density and elastic properties.
* Youngs modulus (GPa) - is a measure of a material's stiffness, defined as the ratio of stress to strain in the linear elastic region of deformation.
* S-wave /shear velocity (m/s) - is the speed at which secondary (shear) seismic waves travel through a material, depending on the material's shear modulus and density.
* Shear modulus / modulus of rigidity (GPa) - is a measure of a material's resistance to shear deformation, defined as the ratio of shear stress to shear strain.

Response Feature:

* cumulative oil production 3 years - the total oil produced by the well over three years of production 

#### Map Data

The following map data are available:

* **2d_ai.npy** - acoustic impedance (AI) inverted from geophysical amplitudes and interpretations. Hint: high AI indicates less oil
* **2d_sand_proportion.npy** - proportion of sand facies over the vertical column, 2D sand proportion map. Hint: high proportion of sand generally results in more production.

Comments:

* 2D maps are regular grids 200 by 200 cells, cell extents are 50m by 50m, extending over the reservoir 
* values indicate the vertically averaged property, vertical resolution is the entire reservoir unit
* the indices follow standard Python convention, original is top left corner, indices are from 0, 1, ..., n-1 and the first index is the row (from the top) and the second index is the column from the left.
* e.g. to select the 5th grid cell in x (column) and the 10th grid cell in y (rows), use ndarray[9,4] in Python (aside, array[10,5] in Matlab). 
* the origin of the 2D data (e.g., array[0,0]) is the center of the top left cell, 25m and 25m along y and x direction (refer to the image above)

### Required Hackathon Submissions

By Wednesday June 18th at 9:30 pm each team must submit:

* **Solution Table** - a .csv file with your predictions for the 10 preproduction wells. The submitted file should follow the format of the provided template [solution.csv](https://github.com/PGEHackathon/mite/blob/main/resources/solution.csv) for automatic scoring.

    * the file must be named 'solution.csv' with final values in a commit and then pushed to Github for the automated scoring.

* **Python Workflow and Associated Files** - commited to this repository with the workflow as a Jupyter Notebook .ipynb file along with all data files required to reproduce your team's solutions. The submitted workflow Jupyter Notebook should follow the format of the provided template [Hackathon_ProjectTemplate](https://github.com/PGEHackathon/mite/blob/main/resources/Hackathon_ProjectTemplate.ipynb) for enhanced workflow communication and code readibility.

* **Presentation** - a PowerPoint slide deck .PPTX file for your team's final presentation to our judges. The submitted presentation should follow the format of the provided example presentation [Hackathon_PresentationTemplate](https://github.com/PGEHackathon/mite/blob/main/resources/Hackathon_PresentationTemplate.pptx).

The Workflow and Presentation submission templates are in the [resources respository](https://github.com/PGEHackathon/resources) and the results submission template is in this repository.

#### Hackathon Schedule

| Day   | Time                  | Topic                                  | Objective                                                                                      |  Notes  | Demo | Interactive | Video |
|-----------|---------------------------|----------------------------------------|------------------------------------------------------------------------------------------------|------|----|------|------|
| Sunday Day 1 | 7:30 PM - 9:30 PM | Welcome, Introduction                        | introduction / overview, energy data science, machine learning basics, set up – github and codespace  | [Introductions](https://github.com/PGEHackathon/mite/blob/main/resources/2025_PGE_HS_Hackathon_Introduction.pdf) [ML Basics](https://github.com/PGEHackathon/mite/blob/main/Pyrcz_Lectures/06_Machine_Learning.pdf)| | | [VS Code](https://youtu.be/1_VefXlsdgA?si=WbIqOCO2kFd9J6SE) [git and Github](https://youtu.be/0xrsyxsI31A?si=OD3tLFoYmzGH_jQV) [Jupyter Notebooks](https://youtu.be/jSNs4I4abKg?si=OCM5J-uh9fJGIhFd) [Machine Learning](https://youtu.be/zOUM_AnI1DQ?si=2zpu43G_PLGn2ttB) |
| Monday Day 2 | 8:30 AM - 10:30 AM | Data Science in Python | Python packages NumPy, SciPy, matplotlib, etc. |    | | |  |
|       | 6:30 PM - 9:30 PM    | Feature Engineering / Feature Imputation | feature imputation, missing data hands on and slides, scikit-learn | [e-book](https://geostatsguy.github.io/MachineLearningDemos_Book/MachineLearning_feature_imputation.html) [notes](https://github.com/PGEHackathon/mite/blob/main/Pyrcz_Lectures/05d_Feature_Imputation.pdf) | [demo](/Pyrcz_ebook/MachineLearning_feature_imputation.ipynb) | [Dashboard](/notebooks/Interactive_Sivia_Coin_Toss.ipynb) | |
| Tuesday Day 3 | 8:30 AM - 10:30 PM | Feature Engineering / Feature Selection | feature engineering, curse of dimensionality and feature ranking  | [e-book](https://geostatsguy.github.io/MachineLearningDemos_Book/MachineLearning_feature_ranking.html) [notes](https://github.com/PGEHackathon/mite/blob/main/Pyrcz_Lectures/05b_Feature_Selection.pdf) | [demo](/Pyrcz_ebook/MachineLearning_feature_ranking.ipynb)| [Dashboard](/notebooks/Interactive_Declustering.ipynb) | [Feature Selection](https://youtu.be/5Q0gemu-h3Q?si=PhgGEQ03QNqXgCFM) |
|       |  2:45 PM - 5:00 PM | Inferential Machine Learning / Cluster Analysis | inferential machine learning, clustering, K-means clustering | [e-book](https://geostatsguy.github.io/MachineLearningDemos_Book/MachineLearning_clustering.html) [notes](https://github.com/PGEHackathon/mite/blob/main/Pyrcz_Lectures/07_Clustering.pdf) | [demo](/Pyrcz_ebook/MachineLearning_clustering.ipynb) |  |  | [Clustering](https://youtu.be/oFE10cLl0Fs?si=8Uruksc4mf2djLEd) |
|       | 6:30 PM - 9:30 PM    | Inferential Machine Learning / Dimensionality Reduction | inferential machine learning, dimensionality reduction, PCA  | [e-book](https://geostatsguy.github.io/MachineLearningDemos_Book/MachineLearning_PCA.html) [notes](https://github.com/PGEHackathon/mite/blob/main/Pyrcz_Lectures/08_DimensionalityReduction.pdf) | [demo](/Pyrcz_ebook/MachineLearning_PCA.ipynb) | | [PCA](https://youtu.be/-to3JXiae9Y?si=YdCk5gwsEQupBoRe) |
| Wednesday Day 4 | 8:30 AM - 9:45 AM     | Predictive Machine Learning | multilinear regression, tree-based methods, decision tree, random forest  | [e-book](https://geostatsguy.github.io/MachineLearningDemos_Book/MachineLearning_linear_regression.html) [linear](https://github.com/PGEHackathon/mite/blob/main/Pyrcz_Lectures/09_LinearRegression.pdf) [tree](https://github.com/PGEHackathon/mite/blob/main/Pyrcz_Lectures/14_DecisionTree.pdf) [forest](https://github.com/PGEHackathon/mite/blob/main/Pyrcz_Lectures/15_EnsembleTree.pdf) | [linear](/Pyrcz_ebook/MachineLearning_linear_regression.ipynb) [tree](/Pyrcz_ebook/MachineLearning_decision_tree.ipynb) [forest](/Pyrcz_ebook/MachineLearning_ensemble_trees.ipynb) | [Dashboard](https://github.com/daytum/geostats_training/blob/main/notebooks/Interactive_Correlation_Coefficient.ipynb) | [ML Prediction](https://youtu.be/EbYePnjWB5o?si=kv7f3Hwlc_Ov4wSP) |
|       | 6:30 PM - 9:30 PM     | Complete Presentations and Submission         | PowerPoint and Jupyter Notebooks  |  |  |  | |
| Thursday Day 5  | 8:30 AM - 10:30 AM     | Final Presentations and Awards   |         |  |  |  | |

