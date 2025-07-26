# Calcium Data Analysis 

This repository contains a Python script used to analyze single-cell calcium imaging data in the context of my bachelor's thesis.

The full Python script used for the analysis is available as an open-source repository on GitHub: [github.com/antonia2510/calcium_analysis_bachelor_thesis](https://github.com/antonia2510/calcium_analysis_bachelor_thesis)

## Content
- AUC calculation 
- Peak amplitude analysis
- basal calcium level analysis 


## Libraries 
- `pandas`
- `numpy`
- `matplotlib`

## Step-by-step procedure
Data analysis of calcium imaging data was performed using Python (version 3.12.7) with the following libraries: pandas, NumPy and matplotlib. Raw fluorescence data given as the ratio F340/F380 for every single cell were imported from Excel files and the corresponding time axis was reconstructed based on the set frame interval of 2 seconds given by the experimental acquisition settings. 


#### Basal calcium level

To determine the basal calcium level, the mean ratio F340/F380 of the first 25 time frames (corresponding to the initial 50 seconds) was calculated for each individual cell. The overall basal calcium level was then obtained by averaging these values across all measured cells. 

To evaluate calcium responses, peak amplitude and area under the curve (AUC) were determined. 
Analyses were conducted separately for thapsigargin and ATP stimulation, using the same algorithm but adjusted parameters. 

#### Data Analysis of thapsigargin and ATP treatment 

To determine the peak amplitude under thapsigargin treatment, the minimum F340/F380 ratio within a pre-defined baseline window was subtracted from the maximum signal observed within a pre-defined search window for each cell individually. Two Peaks were analyzed: Peak 1, corresponding to the ER calcium release following thapsigargin stimulation and Peak 2 representing the calcium influx upon re-addition of extracellular calcium. For Peak 1, the baseline window was set between 20 and 30 seconds and the peak was searched between 60 and 200 seconds. For the second peak, the baseline window was defined from 550 to 560 seconds and the corresponding search window was set from 600 to 770 seconds. 
By calculating the difference between the maximum value in the peak window and the minimum in the corresponding baseline window, the peak amplitude was calculated. By averaging over all calculated peak amplitudes for the regarding peak, the mean peak amplitude for Peak 1 and Peak 2 could be calculated. 


To determine the total calcium response under thapsigargin treatment, the AUC was calculated for two defined search intervals for each single cell.  First, a baseline calcium level was defined as the mean F340/F380 ratio within a pre-defined baseline window (also 20-30 seconds for Peak 1 and 500-510 seconds for Peak 2). A fixed threshold was set by adding 0.002 to the baseline value in order to reduce the influence of baseline noise and prevent premature detection of calcium responses.
The search window for Peak 1 was set to 60-200 seconds and the search window for Peak 2 was defined from 600-720 seconds. Within these defined search windows, the first time point at which the calcium signal exceeded this cell-specific threshold was determined. Starting from this time point, the AUC was calculated over a fixed interval. This fixed interval was defined as 200 seconds for Peak 1 and 150 seconds for Peak 2. The AUC was then calculated using the trapezoidal rule, which is a numerical method, that approximates the area under the curve by segmenting it into a series of trapezoid forms, followed by summing the areas of all trapezoids within the defined interval. This was performed for each cell individually and by averaging over all calculated values, the mean area under the curve for each Peak could be determined. 


The analysis of ATP treatment was performed analogously to the Thapsigargin protocol described above. Baseline and threshold definitions as well as calculation of peak amplitude and AUC was performed following the same procedures. The only difference was the definition of the fixed integration windows for AUC calculations. For Peak 1, a 60 second interval was set and for Peak 2, the AUC was calculated over 140 seconds. All other parameters remained consistent with Thapsigargin analyses. 





All parameters such as baseline and peak windows, AUC integration lengths and the threshold buffer are defined at the beginning of the script and can be adjusted to match different experimental conditions. 




This project is licensed under the MIT License.  
See the [LICENSE](LICENSE) file for details.
