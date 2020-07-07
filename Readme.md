# 11th place solution to the TReNDS Neuorimaging competition

As described in my [kaggle post](https://www.kaggle.com/c/trends-assessment-prediction/discussion/164915), the notebooks contained in this repository contain the code base for my 11th place soltuino for the TReNDS Neuroimaging competition.

The notebooks are separated in the following ways.

Thanks again to the organizers for a great competition and for all my competitors for a great challenge. As my first kaggle competition, I learned a lot and trying to keep up with the top scores was a thrill (while also very stressful)!

I finally was able to write up the (almost) whole code base to my approach. Here's how it worked and what made my approach sometimes unique:

1. [TReNDS: Exploration of the targets](notebook_01_trends-exploration-of-the-targets.ipynb): Having a closer look at the targets I decided for the following transformations.
   - **First**, targets were scaled using a `RobustScaler`.
   - **Second**, targets 2 to 5 were transformed to a more normal distribution using a power of 1.5
   - **Third**, I took the decision to restrict all predictions to the unique values in the target set. Especially for `age` this was helping a lot.
2. [TReNDS: Feature exploration &amp; engineering](notebook_02_trends-feature-exploration-engineering.ipynb): Concerning the feature datasets, I removed about 1% of extrem outliers (i.e. subjects with often very strange feature values) and I've created two additional feature datasets:
   - **Intra subject** features: By computing the correlations between all 53 MRI maps within a subject, I've created 1'378 new features hopefully representing within subject characteristics.
   - **Inter subject** features: By computing the correlation between each of the 53 MRI maps and the corresponding averaged population map, I've created 53 new features hopefully representing between subject characteristics.
3. [TReNDS: Data scaling and modelling](notebook_03_trends-data-scaling-and-modeling.ipynb): Following the lead from the kaggle discussions/notebooks I investigated a feature dataset unique scaling approach. However, instead of scaling the FNC dataset just with a factor of 500, I fine tuned the exact scaling factor for each of my 4 feature datasets. Additionally, this fine tuning was done separately for each of the 5 targets, and for each of the models I've explored (i.e. Ridge and SVR with an RBF kernel).
4. Inspired by the [TReNDS Multi-Layer Model](https://www.kaggle.com/david1013/trends-multi-layer-model) notebook, which I discovered in the last few days of the computation, I've adapted the code to my dataset (see the [stacking notebook](notebook_04_trends-model-stacking.ipynb)). By adapting this code and optimizing it to my individually scaled dataset, I was able to push my score the ladder up to my final position.

As an additional goody, I've also tried to profit from the particular relationship between `domain2_var1` and `domain2_var2` (as described in my first notebook) and was hoping that a multi-target prediction approach could help. To do so, I've implemented a dense neural network with two outputs and multiple loss functions. Unfortunately, this approach wasn't fruitful. Nonetheless, the corresponding notebook can be found here: [Multi-loss neural network for domain2 targets](notebook_05_multi-loss-neural-network-for-domain2-targets.ipynb)


## Exploration of scaling for Ridge

### AGE

    all_combos = [[0.2500],   ## Feature: IC_                 Start
                  [0.0398],   # Feature: _vs_                0.0398  -0.142982
                  [0.0866],   # Feature: corr_coef             0.0866  -0.138965
                  [0.0234],   # Feature: ^c[0-9]+_c[0-9]+     0.0234  -0.140535

### D1_V1

    all_combos = [[0.2500],   # Feature: IC_                 Start
                  [0.0106],   # Feature: _vs_                 0.0106  -0.150447
                  [0.0316],   # Feature: corr_coef             0.0316  -0.150389
                  [0.0188],   # Feature: ^c[0-9]+_c[0-9]+    0.0188  -0.150697

### D1_V2

    all_combos = [[0.1212],   # Feature: IC_                  0.1212  -0.150262
                  [0.0185],   # Feature: _vs_                0.0185  -0.150339
                  [0.0316],   # Feature: corr_coef             0.0316  -0.150242
                  [0.0250],   # Feature: ^c[0-9]+_c[0-9]+    Start

### D2_V1

    all_combos = [[0.2500],   # Feature: IC_                 Start
                  [0.0083],   # Feature: _vs_                 0.0083  -0.180852
                  [0.0121],   # Feature: corr_coef             0.0121  -0.180732
                  [0.0117],   # Feature: ^c[0-9]+_c[0-9]+    0.0117  -0.181082

### D2_2

    all_combos = [[0.2610],   # Feature: IC_                 0.2610  -0.17579
                  [0.0250],   # Feature: _vs_                Start
                  [0.0521],   # Feature: corr_coef            0.0521  -0.175517
                  [0.0224],   # Feature: ^c[0-9]+_c[0-9]+      0.0224  -0.175398


## Exploration of scaling for SVM rbf

### AGE

    all_combos = [[0.2500],   # Feature: IC_                 Start
                  [0.0150],   # Feature: _vs_                0.01496  -0.142924  4.216965
                  [0.0415],   # Feature: corr_coef             0.04145  -0.138763  3.349654
                  [0.0141],   # Feature: ^c[0-9]+_c[0-9]+     0.01413  -0.140380  2.818383

### D1_V1

    all_combos = [[0.2500],   # Feature: IC_                  Start
                  [0.0116],   # Feature: _vs_                   0.01155  -0.150561  0.464159
                  [0.0316],   # Feature: corr_coef             0.03162  -0.150803  0.562341
                  [0.0178],   # Feature: ^c[0-9]+_c[0-9]+     0.01778  -0.150912  0.562341

### D1_V2

    all_combos = [[0.1799],   # Feature: IC_                 0.17988  -0.150310  0.211349
                  [0.0100],   # Feature: _vs_                 0.01000  -0.150280  0.199526
                  [np.nan],   # Feature: corr_coef             No increase
                  [0.0250],   # Feature: ^c[0-9]+_c[0-9]+    Start

### D2_V1

    all_combos = [[0.2500],   # Feature: IC_
                  [0.0251],   # Feature: _vs_                0.02512  -0.181219  0.281838
                  [0.0363],   # Feature: corr_coef            0.03631  -0.180938  0.316228
                  [0.0225],   # Feature: ^c[0-9]+_c[0-9]+      0.02252  -0.180743  0.337115

### D2_2

    all_combos = [[0.1884],   # Feature: IC_                 0.18836  -0.175802  0.223872
                  [0.0250],   # Feature: _vs_                Start 
                  [0.0501],   # Feature: corr_coef             0.05012  -0.175473  0.177828
                  [0.0224],   # Feature: ^c[0-9]+_c[0-9]+     0.02239  -0.175576  0.251189
