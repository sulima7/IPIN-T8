### Long description of the competing system

5G positioning will be part of our lives and it will enable diversified applications in all walks of life. A large number of application scenarios such as the Internet of Vehicles, autonomous driving, smart manufacturing, smart logistics, drones, and asset tracking have higher requirements for positioning capabilities. Excessive errors may lead to poor user experience or other problems. Therefore, we should enhance network positioning technology to improve 5G positioning accuracy.

The challenges we face in Track 8 are the features of raw data provided are inaccurate. These features are the results of processing and it’s so hard to infer more information from these features. What’s more, there exists a mixture of LOS paths, weak LOS paths, and NLOS paths. And there are existing timing errors among the receivers in TRPs, called time alignment errors (TAEs). The TAEs of the TRPs are unknown and different in different datasets. All of the above have caused great difficulties in accurate positioning.

In these cases, we can only use the roughly known environmental information and the mutual location relationship between the base-stations to infer the correct distance. To achieve a more accurate positioning result, we try to introduce a neural network method to get more accurate distance estimations. 

Next, we collect the distances from base-stations to estimate the target's position. We take the base-stations as the center of a circle and the estimated distance as the radius. Candidate positions can be obtained for four base-stations based on the trilateration algorithm. For all these alternative positions, we apply the clustering algorithm to obtain the cluster center, which is the estimated position of the target. 

Finally, we use the SG filter to smooth the trajectory, resample it to get the final positions, and take the Euclidean distance between estimated and accurate results as the primary evaluation metric.

Now we have been exploring and improving our method. We aim to find an end-to-end approach to solve this problem efficiently and accurately.