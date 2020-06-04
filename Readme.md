## Notebook Summary

- [Notebook 1](https://nbviewer.jupyter.org/github/miykael/kaggle_trends_challenge/blob/master/01_preparation_nifti.ipynb): Preparing NIfTI files and extracting a multitude of potential featrues.
- [Notebook 2](https://nbviewer.jupyter.org/github/miykael/kaggle_trends_challenge/blob/master/02_data_exploration.ipynb): Explorative Data Analysis, plus feature selection.
- [Notebook 3a_ridge](https://nbviewer.jupyter.org/github/miykael/kaggle_trends_challenge/blob/master/03a_model_linear_regression_ridge.ipynb): Data Modeling using ridge regression
- [Notebook 3a_age_ridge](https://nbviewer.jupyter.org/github/miykael/kaggle_trends_challenge/blob/master/03a_model_linear_regression_ridge-age.ipynb): Data Modeling using ridge regression with discrete features for age
- [Notebook 3b_sgd](https://nbviewer.jupyter.org/github/miykael/kaggle_trends_challenge/blob/master/03b_model_linear_regression_sgd.ipynb): Data Modeling using sgd
- [Notebook 3b_age_sgd](https://nbviewer.jupyter.org/github/miykael/kaggle_trends_challenge/blob/master/03b_model_linear_regression_sgd-age.ipynb): Data Modeling using sgd with discrete features for age
- [Notebook 3c_linear_SVM](https://nbviewer.jupyter.org/github/miykael/kaggle_trends_challenge/blob/master/03c_model_linear_regression_svr-linear-age.ipynb): Data Modeling using linear SVM
- [Notebook 3c_age_linear_SVM](https://nbviewer.jupyter.org/github/miykael/kaggle_trends_challenge/blob/master/03c_model_linear_regression_svr-linear-age.ipynb): Data Modeling using linear SVM with discrete features for age
- [Notebook 3d_rbf_SVM](https://nbviewer.jupyter.org/github/miykael/kaggle_trends_challenge/blob/master/03d_model_linear_regression_svr-rbf.ipynb): Data Modeling using rbf SVM
- [Notebook 3d_age_rbf_SVM](https://nbviewer.jupyter.org/github/miykael/kaggle_trends_challenge/blob/master/03d_model_linear_regression_svr-rbf-age.ipynb): Data Modeling using rbf SVM with discrete features for age
- [Notebook 4a Neural Network - Exploration](https://nbviewer.jupyter.org/github/miykael/kaggle_trends_challenge/blob/master/04a_model_nonlinear_NN_multi-hp_exploration.ipynb): Using Keras-tuner, different model architectures were explored.
- [Notebook 4b Neural Network - Multi value prediction](https://nbviewer.jupyter.org/github/miykael/kaggle_trends_challenge/blob/master/04b_model_nonlinear_NN_multi.ipynb): Dense Neural Network (Tensorflow: Keras API) was used to predict all 5 target values at once.
- [Notebook 4c Neural Network - Single value prediction](https://nbviewer.jupyter.org/github/miykael/kaggle_trends_challenge/blob/master/04c_model_nonlinear_NN_singular.ipynb): Dense Neural Network (Tensorflow: Keras API) was used to predict each of the 5 target values separately.
- [Notebook 5a Hierarchical Models - Regression](https://nbviewer.jupyter.org/github/miykael/kaggle_trends_challenge/blob/master/05_hierarchical_models_a_regression.ipynb): Result reports from all different models are combined in a hierarchical model approach using ridge or lass regression.
- [Notebook 5b Hierarchical Models - KNN](https://nbviewer.jupyter.org/github/miykael/kaggle_trends_challenge/blob/master/05_hierarchical_models_b_knn.ipynb): Result reports from all different models are combined in a hierarchical model approach using KNN regression.
- [Notebook 5c Hierarchical Models - Random Forest](https://nbviewer.jupyter.org/github/miykael/kaggle_trends_challenge/blob/master/05_hierarchical_models_c_random_forest.ipynb): Result reports from all different models are combined in a hierarchical model approach using Random Forest regression.

## Submission Summary

| Model          | Dataset     | Score | score1 | score2 | score3 | score4 | score5 | ScoreKaggle |
|----------------|-------------|-------|--------|--------|--------|--------|--------|-------------|
| ridge          | merge       | 1590  |   1444 |   1522 |   1506 |   1820 |   1759 |        1604 |
| ridge_age      | merge       | 1588  |   1439 |   1522 |   1506 |   1820 |   1759 |        1603 |
| sgd            | merge       | 1591  |   1450 |   1521 |   1507 |   1819 |   1762 |        1611 |
| sgd_age        | merge       | 1592  |   1451 |   1521 |   1507 |   1819 |   1762 |        1606 |
| svr-linear     | merge       | 1589  |   1444 |   1522 |   1506 |   1820 |   1759 |        1604 |
| svr-linear_age | merge       | 1588  |   1438 |   1522 |   1506 |   1820 |   1759 |        1604 |
| svr-rbf        | merge       | 1602  |   1482 |   1524 |   1507 |   1820 |   1762 |        1612 |
| svr-rbf_age    | merge       | 1600  |   1477 |   1524 |   1507 |   1820 |   1762 |        1614 |
| nn-multi       | merge       | 1631  |        |        |        |        |        |        1648 |
| nn-singular    | merge       | 1610  |   1470 |   1530 |   1537 |   1832 |   1779 |        1634 |
| ridge          | short_merge | 1571  |   1439 |   1500 |   1477 |   1799 |   1733 |        1611 |
| ridge_age      | short_merge | 1570  |   1435 |   1500 |   1477 |   1799 |   1733 |        1613 |
| sgd            | short_merge | 1572  |   1450 |   1503 |   1471 |   1787 |   1734 |        1614 |
| sgd_age        | short_merge | 1570  |   1445 |   1503 |   1471 |   1787 |   1734 |        1616 |
| svr-linear     | short_merge | 1571  |   1439 |   1500 |   1477 |   1799 |   1733 |        1611 |
| svr-linear_age | short_merge | 1570  |   1435 |   1500 |   1477 |   1799 |   1733 |        1613 |
| svr-rbf        | short_merge | 1585  |   1473 |   1504 |   1488 |   1798 |   1741 |        1619 |
| svr-rbf_age    | short_merge | 1584  |   1469 |   1504 |   1488 |   1798 |   1741 |        1618 |
| nn-multi       | short_merge | 1619  |        |        |        |        |        |        1651 |
| nn-singular    | short_merge | 1596  |   1470 |   1518 |   1501 |   1819 |   1760 |             |
| hierarchical   | ridge       |       |        |        |        |        |        |             |
| hierarchical   | lasso       |       |        |        |        |        |        |        1719 |
| hierarchical   | KNN         |       |        |        |        |        |        |        1686 |
| hierarchical   | rand.forest |       |        |        |        |        |        |             |
| baseline+age1  | ridge       |       |        |        |        |        |        |             |
| baseline+age2  | ridge_age   |       |        |        |        |        |        |             |
