# **New York City Taxi Fare Prediction - TOP 2% TEAM!**
- **Author: Chongzheng Zhao**
- **Kaggle Competition - New York City Taxi Fare Prediction**
- **FINAL BEAT 1454 TEAMS!**
- **We team NYCTAXI located at 30 out of 1484 teams, Top 2%!**
- **Final Score 2.86770**
- **Competition Official Website: https://www.kaggle.com/c/new-york-city-taxi-fare-prediction**
- **To see the leaderboard(competition result): https://www.kaggle.com/c/new-york-city-taxi-fare-prediction/leaderboard**
- **Welcome to my Github Profile: https://github.com/ChongzhengZhao/**
- **Welcome to my Kaggle Profile: https://www.kaggle.com/chongzhengzhao**
- **Welcome to my Linkedin Profile: https://www.linkedin.com/in/chongzhengzhao/**
- **Last updated: 30/11/2018**


# ***·项目概要***
按照项目步骤，拿到Raw Data后，按照顺序进行data预处理、feature engineering（特征工程）、做model（模型）、ensemble and stacking。
# ***·Data简介***
 1. New York City Taxi Fare Prediction项目的数据集将近有55million rows，这在kaggle比赛中算比较大的数据集了，这种数据集需要在性能较高电脑中才能处理效率高，并且数据大带来的model调参也比较困难
 2. DATA KEY， FEATURES ADN TARGET
    key -  
        Unique string identifying each row in both the training and test sets. Comprised of pickup_datetime plus a unique integer, but this doesn't matter, it should just be used as a unique ID field. Required in your submission CSV. Not necessarily needed in the training set, but could be useful to simulate a 'submission file' while doing cross-validation within the training set.
    Features - 
        pickup_datetime - timestamp value indicating when the taxi ride started.
        pickup_longitude - float for longitude coordinate of where the taxi ride started.
        pickup_latitude - float for latitude coordinate of where the taxi ride started.
        dropoff_longitude - float for longitude coordinate of where the taxi ride ended.
        dropoff_latitude - float for latitude coordinate of where the taxi ride ended.
        passenger_count - integer indicating the number of passengers in the taxi ride.
    Target - 
        fare_amount - float dollar amount of the cost of the taxi ride. This value is only in the training set; this is what you are predicting in the test set and it is required in your submission CSV.
# ***·Data预处理***
1. data中有很多data outlier无效数据，要drop掉那些数据，使得model进行训练的时候使用正确数据进行，得到的model更准确。
2. drop掉的无效数据有：值为NA（无记录）的订单记录、费用小于0美金及费用大于475美金的订单记录、上车地点经度小于-80和大于-70的订单记录、上车地点纬度小于35和大于45的订单记录、下车地点经度小于-80和大于-70的订单记录、下车地点纬度小于35和大于45的订单记录、乘客数小于0位和大于等于10位的订单记录。【再看一下LGB代码的】
# ***·Feature Engineering（特征工程）：增加新特征、观察特征对模型的contribution、增强特征重要性高的特征***
1. 特征：distance
    利用manhattan distance、Straight distance、Haversine formula for distance、Bearing Distance计算distance
2. 特征：pickup_datetime
3. 特征：hour_of_day
4. 特征：month
5. 特征：year
6. 特征：weekday
7. 特征：day_of_month
8. 特征：利用manhattan distance计算上车点到肯尼迪机场、纽瓦克自由国际机场、纽约LaGuardia Airport、自由女神像、纽约市中心的距离
9. 特征：利用Haversine formula for distance计算上车点到肯尼迪机场、纽瓦克自由国际机场、纽约LaGuardia Airport、自由女神像、纽约市中心的距离
# ***·Modelling（模型）***
1. 概述：模型采用LightGBM、XGBoost，并利用Bayesian-optimization来调整每个模型的参数
2. 每个模型都有参数，跑完模型后会得到rmse值，rmse（均方根误差亦称标准误差），rmse越小，代表与真实误差越小，排名越靠前。
3. 模型做完后，可以生成feature importance图表，看之前feature engineering中加入的feature对模型结果有没有帮助
4. XGBoost速度比LightGBM慢一些，feature importance的代码与LightGBM不一样
# ***·Ensemble and Staking***
1. 将每个model调整到rmse最优最小的时候，就可以进行这步操作。这步操作通常就是将多种模型进行结合，互相弥补，以达到更好的结果。
2. 这部分原理见Document。
# ***·NOTE***
本地查看到的rmse并不是上传到kaggle竞赛平台的最后rmse分数。用于预测的test集中并不包含fare amount，我们的model就是基于各种feature去预测打车的费用，所以我们上传到平台的是打车费用，他们后台会匹配我们预测的结果和后台真实值的匹配度，以计算排名和分数。
