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

| Day   | Time                  | Topic                                  | Objective                                                                                      |  Notes  | Demo | Interactive |
|-----------|---------------------------|----------------------------------------|------------------------------------------------------------------------------------------------|------|----|------|
| Sunday Day 1 | 7:30 PM - 9:30 PM | Welcome, Introduction                        | introduction / overview, energy data science, machine learning basics, set up – github and codespace                               | [Overview](/pdfs/CourseOverview.pdf) | | |
| Monday Day 2 | 8:30 AM - 10:30 AM | Data Science in Python | Python packages NumPy, SciPy, matplotlib, etc. | [Introduction](/pdfs/Introduction.pdf)    | | |
|       | 6:30 PM - 9:30 PM    | Feature Engineering / Feature Imputation | feature imputation, missing data hands on and slides, scikit-learn                                          | [Notes](/Pyrcz_UTCourse/02_Probability.pdf) | | [Dashboard](/notebooks/Interactive_Sivia_Coin_Toss.ipynb) |
| Tuesday Day 3 | 8:30 AM - 10:30 PM | Feature Engineering / Feature Selection | feature engineering, curse of dimensionality and feature ranking  | [Notes](/Pyrcz_UTCourse/09b_Spatial_Debias.pdf) | [Demo](/notebooks/declustering.ipynb)| [Dashboard](/notebooks/Interactive_Declustering.ipynb) |
|       |  2:45 PM - 5:00 PM | Inferential Machine Learning / Cluster Analysis | inferential machine learning, clustering, K-means clustering | | [Notes](/Pyrcz_UTCourse/05_Univariate_Distributions.pdf) | [Demo](/notebooks/bootstrap.ipynb) | [Dashboard](/notebooks/Interactive_Bootstrap.ipynb) |
|       | 6:30 PM - 9:30 PM    | Inferential Machine Learning / Dimensionality Reduction | inferential machine learning, dimensionality reduction, PCA                                                                                                 |  | | |
| Wednesday Day 4 | 8:30 AM - 9:45 AM     | Predictive Machine Learning | multilinear regression, tree-based methods, decision tree, random forest  | [Notes](/Pyrcz_UTCourse/08_Bivariate_Correlation.pdf) | [Demo](/notebooks/multivariate_analysis.ipynb) | [Dashboard](https://github.com/daytum/geostats_training/blob/main/notebooks/Interactive_Correlation_Coefficient.ipynb) |
|       | 6:30 PM - 9:30 PM     | Complete Presentations and Submission         | PowerPoint and Jupyter Notebooks  | [Notes](/Pyrcz_UTCourse/10_Spatial_Calc.pdf) | [Demo](/notebooks/variogram_calculation.ipynb) | [Dashboard](/notebooks/Interactive_Variogram_Calculation.ipynb) |
| Thursday Day 5  | 8:30 AM - 10:30 AM     | Final Presentations and Awards   |         |  | [Demo](/notebooks/variogram_modeling.ipynb) |  |

