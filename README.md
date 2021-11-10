# Anime Recommender System
 A Machine learning model that uses collaborative filtering to recommend anime to users, written in python using PyTorch, NumPy and Pandas.

# Dataset and preprocessing
The dataset used was a subset of the [MyAnimeList dataset](https://www.kaggle.com/azathoth42/myanimelist) which contains around 80 million ratings of 14k anime by 300k users. The 5,000 most popular anime and 100,000 randomly sampled users who rated at least 50 anime were taken as the "cleaned up" dataset with which latent features were trained on. <br>
[Dask](https://dask.org) was used to process the relatively large dataset in a distributed way. You can find the code for this in [MAL Dataset/Dataset prep.ipynb](https://github.com/greenfish8090/Anime-Recommender-System/blob/main/MAL%20Dataset/Dataset%20prep.ipynb).

# Training
Matrix factorization is at the heart of this algorithm. The 5,000 x 100,000 dimensional sparse ratings matrix is decomposed into a 5,000 x 10 dimensional 'anime_matrix' and a 10 x 100,000 dimensional 'user_matrix'. These matrices are initialized at random, and are iteratively updated to converge them such that their product matches the original ratings matrix. With this, we will have essentially "filled in" the missing ratings. <br>
PyTorch was used in order to leverage the GPU and speed up training significantly. I also used autograd and an optimizer from PyTorch because why not <br>
Walkthrough and code can be found in [Training.ipynb](https://github.com/greenfish8090/Anime-Recommender-System/blob/main/Training.ipynb)

# Prediction
When we need to recommend anime to a user that wasn't part of the 100,000 trained users, we fetch their profile from MyAnimeList using [jikanpy](https://github.com/abhinavk99/jikanpy), train their specific 10 x 1 vector and then use that to predict their ratings.<br>
The code for this is in [Predict.ipynb](https://github.com/greenfish8090/Anime-Recommender-System/blob/main/Predict.ipynb)

#### Thanks for reading!
