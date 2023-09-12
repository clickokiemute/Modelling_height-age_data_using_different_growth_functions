# Modelling_height-age_data_using_different_growth_functions
Modelling height-age data using different forest tree growth functions


INTRODUCTION

This report work/home task, focuses on analysing forest type data, MSMA and the mathematical properties of the growth function model by Levakovic II (1935), (passing zero-point, increment function, asymptote, inflection point) and estimating function parameters for the forest type height-age data. 

The essence for this analysis and others on growth function models, is to simulate and hence understand properly, what is attainable in real life situations, using abstractions or models.

For the analysis, we will use Rstudio, which is the script environment for data analysis, using  R programming.


MATERIALS AND METHODS

The forest type data (ekMSMA and eyMSMA) been analysed, is from the Estonian authorities responsible for disseminating forest data. And we analysed this forest data, to get the following information;

i.	Number of stands in development class L
ii.	Area of development class L
iii.	Average area of pole stands
iv.	Excluding stands with area equal to zero (0)
v.	An overview of the main specie (Scots pine - MA), etc.

The growth model been analysed is the Levaokovic II growth model 3.6 (1935) as used in the research report, Funciones de crecimiento de aplicación en el ámbito forestal, by Professor Andres Kiviste et al. 

The Levakovic growth model has been used by several other professionals for predicting growth functions in other areas of sciences, aside forestry. One of such, is

1.	Generalized Modified Levakovic Growth Function for Aquatic Species by Deniz Ioena

The following mathematical properties of the Levakovic growth model will be analysed,
i.	Passing zero-point
ii.	Increment function
iii.	Asymptote and 
iv.	Inflection point

For these analysis, we will employ the use of R programming, using Rstudio. 
R programming is preferred over other applications and programming languages for this and other data sciences report/reserch, because of its ability to produce ready business infographics, reports and ML-powered web applications.


RESULTS

After running the analysis in Rscript for the forest plot data, eyMSMA, we came up with the following output;

Data Analysis (Parameters)	Output
Number of stands in developement class L and h100=0 in the dataset	None
Area of development class = L	2156.46 hectares
Average area of pole stands	1.625064 hectares
Exclude stands with zero area from the data set	This should return total number of observations and variables in dataset, as there are no stands with area zero (0)

Other results on the various analysis can be gotten from the Rscrip attached as appendix I in appendices.

Scatter plots for the various developments classes were made and the following results obtained;

•	Treeless area (arengukl=A), showed an unusual tree growth of just 1.0m in about 11 years of age (Plot attached as appendix II).

•	Development class, S (under regeneration) shows a stand attaining an impressive height of approximately 5m at about 18 years of age, compared to others that have average heights of about 2.8m (Plot attached as appendix III).

•	Stands in development class N (young stands), attained growth height of  0 to 8m between ages 0-30, with two stands between ages 44 and 50 performing poorly to have attained the same height range (Plot attachedd as appendix IV).

•	Pole stands in development class L, performed somewhat uniformly, attaining heights of 5-17m between ages 10-60 (Plot attached at appendix V).

Scatter plots for the other development classes are attached as appendices for referencing and subsequent result interpretations.

Plots from scots pine plantation, presented the following results;


 

Figure 8

 

Figure 9

 
Figure 10

GROWTH MODEL 3.6 BY LEVAKOVIC II (1935)

Upon running analysis for the mathematical properties of the Levakovic growth model (M3.6<-nls(h~aa*(a/(bb+a))^cc), using initial values of aa=26,bb=8,cc=2.1, outputs the error - number of iterations exceeded maximum of 50, implying that the model failed to converge. Several reasons could be responsible for this, such as;
I.	Bad start values of parameters
II.	Data are scattered and there are relationships between parameters

To make up for this error, we tried simplification of the model by fixing one of the growth function parameters, in this case, assigning cc=2. After making this adjustment, the estimation/model, converged. We then went on to vary parameter cc further, using 1.5 and 3, although the model predictions do not depend much on that.

From the analysis and plots, the Levakovic II’s growth model produced the following mathematcal porperties;

Mathematical Properties	Results
Passing zero-point	Passing zero point is when age is 0
Increment function	c.c=y^1=abcdt^cd-1/(b+t^c)^d+1
Asymptote	ML2<-nls(h~aa*(a/(bb+a))^2,data=H,start=list(aa=26,bb=8,cc=2))
Summary(ML2)
aa=34 (Asymptote)
Inflection Point	
After calculating new predictions and pltotting the line, we got an Inflection point of 30
Residual standard 
error	2.434 on 44591 degrees of freedom
Number of iterations 
to convergence	6
Achieved convergence tolerance	8.186e-06



The line graph below (Figure 11), gives more insight into the mathematical properties of merging the 3.6 Levakovic II (1935) growth model with the eyMSMA forest data.

 

Figure 11


CONCLUSION

Based on the results of the various analysison plot data MSMA and the Growth function model by Levakovic II (1935), we concluded that;
	The Levakovic function does not fit with MSMA height/age data well! 

	Using cex parameter is needed to increase axes text size fonts.

The data analysis results, provides the necessary information needed for the authorities and other concerned personnel to make further decisions for the benefits of the forest sector in the area under studies.
