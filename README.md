### Long description of the competing system

Description of our algorithm
The technical route used by Mobile Team is mainly based on a machine learning approach. Figure 1 shows the pipeline of our proposed solution. First, we generate simulated data based on data statistics for data augmentation, form the training dataset and then use CatBoost [1] to complete the end-to-end positioning task. Then the position estimation is further corrected based on the room layout and spatio-temporal continuity of the trajectory. Finally, we use the Kalman filter to smooth the trajectory and resample it in real time.

a) Data Analysis and Preparation
The data provided by Track 8 include the timestamps and eight features which are the RTOA and RSRP estimated by the four pRRUs. Note that there are timing errors among the receivers in pRRUs, called time alignment errors (TAEs). The unknown TAEs greatly affect the accuracy of TOA and further the position estimation results, and it is also time-varying among different datasets. In contrast, RSRP is more stable, because data in all data sets are collected in the same environment. In this case, we pay more attention to employing the RSRP and regard it as the key feature.
To fully capture the RSRP feature, we plan to use an ML-based approach to derive the user position. However, we quickly find that the labeled dataset provided by Track 8 is too small. Thus, we apply the interpolation method to augment the labeled data. And then, we quantify the relationship between the RSRP received by each pRRU and the distance in the real data, and the relationship between the RSRP difference and the real distance difference of each pRRU.

Based on these relationships, we can generate many trajectories in a simulated experimental environment and obtain the corresponding simulated RSRP. Meanwhile, we have verified the effect of our simulation method on the real data set. For the interpolated real trajectory in the data set of Testing_B, the RSRP generated by our simulation algorithm has the similar distribution with the real RSRP.

b) ML-based Position Estimation
When we have enough data to form the training dataset, we introduce the Catboost to complete the end-to-end position estimation task. CatBoost is a supervised learning algorithm based on Gradient Boosting and has excellent performance while reducing overfitting and the time spent on tuning. The CatBoost model takes the true coordinate [x_t,y_t ] as a label and the RSRP and the differences of RSRPs received by two different pRRUs as the input vector where the N means that there are N pRRUs while R_(i-1)^t means that the RSRP received by the ⅈth pRRU at time t.
c) Position Estimation Correction
Using CatBoost, we can estimate a position based on RSRP, however, RSRP has large random noise that makes the estimation unstable. To achieve more stable estimation, we use additional information to optimize the position estimation. For example, the users cannot pass through obstacles (e.g., furniture) because of space constraints that can be inferred from the reachable area and the trajectory in the dataset. Furthermore, due to time constraints, it is unlikely that the two adjacent estimated positions are far apart. Therefore, we would correct the abnormal position estimation based on the reachable area, historical position information, and motion direction.
d) Smoothing and Resampling Trajectory
With these data processing methods, we can obtain relatively reliable and stable position estimation. However, the normal trajectory should be smooth and continuous. Thus, we use the Kalman filter which is one of the most important estimation algorithms to real-time smooth the trajectory. Then, we fit the relationship between the recent time and the estimated position (x, y), respectively, and resample it to obtain the results required by the competition.
Lessons Learnt
For Track 8, we propose an end-to-end solution based on a machine learning approach. Moreover, we use statistical knowledge to augment original data and generate simulated data so that the model could be effectively trained. We believe that if there are more real data as the training dataset, the CatBoost can perform better. However, the current solution does not integrate TOA information well and the trained CatBoost model is unable to cope with the unknown environment. 
