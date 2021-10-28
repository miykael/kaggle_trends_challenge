# 11th place solution to the TReNDS Neuorimaging competition

As described in my [kaggle post](https://www.kaggle.com/c/trends-assessment-prediction/discussion/164915), the notebooks contained in this repository contain the code base for my 11th place soltuino for the TReNDS Neuroimaging competition.

The notebooks are separated in the following ways.

Thanks again to the organizers for a great competition and for all my competitors for a great challenge. As my first kaggle competition, I learned a lot and trying to keep up with the top scores was a thrill (while also very stressful)!

I finally was able to write up the (almost) whole code base to my approach. Here's how it worked and what made my approach sometimes unique:

1. [TReNDS: Exploration of the targets](https://nbviewer.jupyter.org/github/miykael/kaggle_trends_challenge/blob/master/notebook_01_trends-exploration-of-the-targets.ipynb): Having a closer look at the targets I decided for the following transformations.
   - **First**, targets were scaled using a `RobustScaler`.
   - **Second**, targets 2 to 5 were transformed to a more normal distribution using a power of 1.5
   - **Third**, I took the decision to restrict all predictions to the unique values in the target set. Especially for `age` this was helping a lot.
2. [TReNDS: Feature exploration &amp; engineering](https://nbviewer.jupyter.org/github/miykael/kaggle_trends_challenge/blob/master/notebook_02_trends-feature-exploration-engineering.ipynb): Concerning the feature datasets, I removed about 1% of extrem outliers (i.e. subjects with often very strange feature values) and I've created two additional feature datasets:
   - **Intra subject** features: By computing the correlations between all 53 MRI maps within a subject, I've created 1'378 new features hopefully representing within subject characteristics.
   - **Inter subject** features: By computing the correlation between each of the 53 MRI maps and the corresponding averaged population map, I've created 53 new features hopefully representing between subject characteristics.
3. [TReNDS: Data scaling and modelling](https://nbviewer.jupyter.org/github/miykael/kaggle_trends_challenge/blob/master/notebook_03_trends-data-scaling-and-modeling.ipynb): Following the lead from the kaggle discussions/notebooks I investigated a feature dataset unique scaling approach. However, instead of scaling the FNC dataset just with a factor of 500, I fine tuned the exact scaling factor for each of my 4 feature datasets. Additionally, this fine tuning was done separately for each of the 5 targets, and for each of the models I've explored (i.e. Ridge and SVR with an RBF kernel).
4. Inspired by the [TReNDS Multi-Layer Model](https://www.kaggle.com/david1013/trends-multi-layer-model) notebook, which I discovered in the last few days of the computation, I've adapted the code to my dataset (see the [stacking notebook](https://nbviewer.jupyter.org/github/miykael/kaggle_trends_challenge/blob/master/notebook_04_trends-model-stacking.ipynb)). By adapting this code and optimizing it to my individually scaled dataset, I was able to push my score the ladder up to my final position.

As an additional goody, I've also tried to profit from the particular relationship between `domain2_var1` and `domain2_var2` (as described in my first notebook) and was hoping that a multi-target prediction approach could help. To do so, I've implemented a dense neural network with two outputs and multiple loss functions. Unfortunately, this approach wasn't fruitful. Nonetheless, the corresponding notebook can be found here: [Multi-loss neural network for domain2 targets](https://nbviewer.jupyter.org/github/miykael/kaggle_trends_challenge/blob/master/notebook_05_multi-loss-neural-network-for-domain2-targets.ipynb)
