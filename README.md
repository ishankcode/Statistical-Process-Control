# Statistical-Process-Control

----
#### <ins>Tools</ins>
1. Python - Pandas, Numpy, Matplotlib, Scipy
2. Excel

----

### <ins> Project Objective :</ins>

To set up a monitoring scheme for future data
---

#### <ins>Data Analysis</ins>
Manurfacturing data contains 209 features. Because of the presence of high dimensionality in the data, the noise of each individual component can add up to a significant amount in the signal-to-noise ratio. This aggregated noise can overwhelm the signal effect, making it difficult to reject the null hypothesis (𝜇1≠𝜇𝑜). This is referred to as the “curse of dimensionality”. 

Used Principal Component Analysis (PCA) as a dimension reduction tool to identify the most important features using Minimum Description Length (MDL), scree plot, and Pareto plot. Based on this analysis, we identified 4 Principal components to be used in our detection process.
![image](https://github.com/ishankcode/Statistical-Process-Control/assets/66678343/623aea69-faf7-41b9-a6cc-eb01815e43cb)

----

#### <ins>Identifying Out of Control Data Points</ins>
Phase I Analysis: It is used to identify the in-control data which are used to estimate the distribution parameters. In this case, Phase I analysis was conducted considering the sample size (n) equal to 1 as each variable has a unique observational value in each sample data set. At first, the chart is applied to the given data to verify the data points are in control and to identify all the out-of-control points. In the next step, we remove all the out-of-control data points and iterate until all the data points are in control.

1. Approach 1:  Multivariate Analysis: 

    - Hotelling T2 chart: T2 has the advantage of being sensitive to spike-type change fluctuations in existing correlated data, but it cannot identify the             disparity created by the process's sustained mean shift. This necessitated the use of additional multi-variate control charts, such as them-CUSUM or m-            EWMA, which are sensitive to mean shift in a process. Will used these in next step.

        ![image](https://github.com/ishankcode/Statistical-Process-Control/assets/66678343/0e8ec186-15b5-42d9-ab6d-2c6eeb9b396c)

         
     - m-CUSUM chart: A cumulative sum (CUSUM) chart is a control chart that is used to enhance the sensitivity of detection in the presence of a small      sustained mean shift.
![image](https://github.com/ishankcode/Statistical-Process-Control/assets/66678343/1dd8f559-c2cb-44d3-8169-c6b0ff6177de)

     - Repeated T^2 Analysis : Until all out of control points are not eliminated Phase-1 analysis is continued.

![image](https://github.com/ishankcode/Statistical-Process-Control/assets/66678343/bf418f11-34f4-4060-b0e1-912687a32976)

    - Final m-CUSUM chart: After finishing Phase I analysis with the m-CUSUM control chart, total in-control samples are 442
    
2. Approach 2- Multiple Univariate Analysis: </br>
In this method, multiple univariate analysis was performed on the first four principal components derived from the prior results. The primary advantage of using multiple univariate charts on principal components is that it eliminates all correlations. As a result, monitoring individual PC’s is advantageous since it ensures that any association between original data is not neglected.

![image](https://github.com/ishankcode/Statistical-Process-Control/assets/66678343/ea8dfd27-a177-44b9-8fc3-301e3021fdab)

Similar to apprach a itterative steps needs to be performed to remove all out of control points. Results summarized in image below.
![image](https://github.com/ishankcode/Statistical-Process-Control/assets/66678343/a5dbaa7a-420b-4835-bf1d-c254eac77ccd)

Based on this analysis we decide to proceed with decision Rule 1 even though the Type 1 error is inflated because of the limitation of data table included in the slides to estimate UCL value based on ARL0 and p. To rectify this mistake in future Monte Carlo simulation can be done to estimate UCL for such high ARLo value.

3. Final Model Selction:

    i) The application of multiple univariate analysis on principal components is beneficial because correlation among the process parameters is eliminated. Thus,        analysis can be done more easily.
    
     ii) Another benefit is, in approach 2 smaller number of points are removed to achieve the in-control state as compared to approach 1, so parameters calculated         for future state will be more accurate as we have relatively more data points for estimation.
