# Modelling_height-age_data_using_different_growth_functions
Modelling height-age data using different forest tree growth functions


 
 

ESTONIAN UNIVERSITY OF LIFE SCIENCES
Institute of Forestry and Engineering



Samuel Okiemute Akporedafe


FOREST GROWTH FUNCTION
(on the growth model by LEVAKOVIC II and MSMA forest type data)


METSA KASVUFUNKTSIOONID
(kasvumudelil LEVAKOVIC II ja MSMA metsatüüpide andmete järgi) 



Home Task 9
Curricula Planning and analysis in multifunctional forestry




Supervisor: Professor Andres Kiviste





Tartu 2022

TABLE OF CONTENT

INTRODUCTION................................................................................................................. 3 
MATERIALS AND METHODS…………………..….. ..................................................... 4
RESULTS………………………………………………………………………….............. 5
CONCLUSIONS................................................................................................................... 9 
APPENDIXES..................................................................................................................... 10 





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


APPENDICES

Appendix I
#########################################
# Home Task 9 - December 2, 2022        #
#########################################

rm(list=ls())  # Delete R objects created during the session 
cat("\014")    # Or Ctrl+L - Clear the Consol window
# Delete Graphic window in Rstudio
if (!is.null(dev.list())) dev.off(dev.list()["Rstudio"]) 


setwd("C:/Users/User/Desktop/MetsMud2022")
dir()

EY<-read.csv2("eyMSMAest.csv",stringsAsFactors = F) # Whole stand data 
EK<-read.csv2("ekMSMAest.csv",stringsAsFactors = F) # Data by stand elements (composition)

##########################################
# A Brief overview of stand data EY      #
##########################################

# How many stands dev.class="L" and h100=0 in our data set?

nrow(subset(EY,arengukl=="L" & h100==0))

# Area of dev.class=L
L<-subset(EY,arengukl=="L")
sum(L$pindala)

# Average area of pole stands
mean(L$pindala)
sum(L$pindala)/length(L$pindala)
sum(L$pindala)/nrow(L)

sum(L$pindala==0)
X<-subset(L,pindala==0)


summary(EY$pindala)
# There is one record (row) with pindala=0, let's exclude it 
EY<-subset(EY,pindala>0)

# Select necessary variables from EY
H<-subset(EY,select=c(id,pindala,h100,arengukl,m1_ha))
# Look at variable distributions  
table(H$arengukl) 
summary(H$h100)    # h100=0 for great number of stands

summary(H$m1_ha)   # Maximum volume is too high
sum(H$m1_ha>1000)  # Only one stand, evidently erratic
# Remove this error 
H<-subset(H,m1_ha<1000)
nrow(H$pindala)
length(H)

#############################################################
# A brief overview of main species (in composition data EK) #
#############################################################
# Select the main tree species data only
EK1<-subset(EK,enamus==1)  # enamus = indicator of main species
# Check, the main species must be Scots pine (MA)
table(EK1$pl)
# There are few other tree species also (errors), exclude them
EK1<-subset(EK1,pl=="MA")
table(EK1$pl)  

# Check storey
table(EK1$ri)
# Exclude data records with ri!="1"
EK1<-subset(EK1,ri=="1")
table(EK1$ri)

# Look at distribution of stand origin 
# (par="I" - planted, "K" - seeded, "S" - natural seed,
# "V" - natural from roots, "X" - not clear)
table(EK1$par)

# Look at age (a)
summary(EK1$a)
table(EK1$a)
hist(EK1$a)
sum(EK1$a==0)
# Exclude stands with zero age
EK1<-subset(EK1,a>0)
summary(EK1$a)

############################################
# Merge data frames H and EK1 and          #
# continue excluding errors and outliers   #
############################################

# Before to merge, check : id in EK1 must be unique!
length(unique(EK1$id))==nrow(EK1) # Must be TRUE
# Merge stand data (H) and main species data (EK1)
# Key to join H and EK1 - column id in both data frames
H<-merge(H,EK1)

# Look at distribution by development classes (arengukl)
table(H$arengukl)

# Treeless area (arengukl="A") should a=0 and h=0
plot(h~a,data=subset(H,arengukl=="A"),xlim=c(0,max(a)),ylim=c(0,max(h)))
subset(H,arengukl=="A")

# Look at development class S = under regeneration
plot(h~a,data=subset(H,arengukl=="S"),xlim=c(0,max(a)),ylim=c(0,max(h)))
# Data points cover each other: use jitter() to add artifical variation 
plot(jitter(h)~jitter(a),data=subset(H,arengukl=="S"),
     xlim=c(0,max(a)),ylim=c(0,max(h)))

# Look at development class N = young stands
plot(jitter(h)~jitter(a),data=subset(H,arengukl=="N"),
     xlim=c(0,max(a)),ylim=c(0,max(h)))
# One stand h is evidently erratic (remove it)
H<-subset(H,!(h>20 & arengukl=="N"))
plot(jitter(h)~jitter(a),data=subset(H,arengukl=="N"),
     xlim=c(0,max(a)),ylim=c(0,max(h)))

# Look at development class L = pole stands
plot(jitter(h)~jitter(a),data=subset(H,arengukl=="L"),
     xlim=c(0,max(a)),ylim=c(0,max(h)))
# Stand with age<10years and height>10m should be erratic
H<-subset(H,!(a<10 & h>10 & arengukl=="L"))
plot(jitter(h)~jitter(a),data=subset(H,arengukl=="L"),
     xlim=c(0,max(a)),ylim=c(0,max(h)))

# Look at development class K = middle age stands
plot(jitter(h)~jitter(a),data=subset(H,arengukl=="K"),
     xlim=c(0,max(a)),ylim=c(0,max(h)))

# Look at development class V = prematured stands
plot(jitter(h)~jitter(a),data=subset(H,arengukl=="V"),
     xlim=c(0,max(a)),ylim=c(0,max(h)))


# Look at development class Y = matured stands
plot(jitter(h)~jitter(a),data=subset(H,arengukl=="Y"),
     xlim=c(0,max(a)),ylim=c(0,max(h)))

# Look at share of main tree species (koef)
summary(H$koef)
# Exclude stands having pine share < 50%
H<-subset(H,koef>=50)

#############################################
# Create the height-age scatterplot         #
#############################################
plot(jitter(h)~jitter(a),data=H,pch=20,cex=0.2)
plot(h~a,data=H,pch=20,cex=0.2)

plot(jitter(h,amount=0.5)~jitter(a,amount=0.5),data=H,pch=20,cex=0.2)

# Create the final figure
plot(NULL,xlim=c(0,250),ylim=c(0,35),
     xlab="Stand age (year)",ylab="Height (m)",
     main="Stand height-age relationship in Rhodococcum site type")
grid()
points(jitter(h,amount=0.5)~jitter(a,amount=0.5),data=H,pch=20,cex=0.2)

# Create separate figure by stand origin

###########################
# Scots pine plantations  #
###########################
plot(NULL,xlim=c(0,250),ylim=c(0,35),
     xlab="Stand age (year)",ylab="Height (m)",
     main="Stand height-age relationship of Scots pine plantations
     in Rhodococcum site type")
grid()
points(jitter(h,amount=0.5)~jitter(a,amount=0.5),
       data=subset(H,par=="I"),pch=20,cex=0.2,col="red")

###########################
# Scots pine seeded       #
###########################
plot(NULL,xlim=c(0,250),ylim=c(0,35),
     xlab="Stand age (year)",ylab="Height (m)",
     main="Stand height-age relationship of seeded Scots pine stands
     in Rhodococcum site type")
grid()
points(jitter(h,amount=0.5)~jitter(a,amount=0.5),
       data=subset(H,par=="K"),pch=20,cex=0.2,col="blue")

#######################################
# Scots pine natural regeration       #
#######################################
plot(NULL,xlim=c(0,250),ylim=c(0,35),
     xlab="Stand age (year)",ylab="Height (m)",
     main="Stand height-age relationship of naturally regerated
     Scots pine stands in Rhodococcum site type")
grid()
points(jitter(h,amount=0.5)~jitter(a,amount=0.5),
       data=subset(H,par=="S"),pch=20,cex=0.2,col="darkgreen")


#################################################################
#################################################################
## Modelling height-age data using different growth functions  ##
#################################################################
#################################################################

# Let's try to estimate the Levakovic function parameters
ML1<-nls(h~aa*(a/(bb+a))^cc,data=H,start=list(aa=26,bb=8,cc=2.1))
# Error in nls(h ~ aa * (a/(bb + a))^cc, data = H, start = list(aa = 26,  : 
# number of iterations exceeded maximum of 50

# One option could be simplification of the model by fixing one of the
# growth function parameters, e.g. assigning cc=2
ML2<-nls(h~aa*(a/(bb+a))^2,data=H,start=list(aa=26,bb=8))
summary(ML2)
# The estimation convergged now!
# aa=34  (asymptote) 
# bb=19
# cc=2

# Calculate new predictions
A<-1:250
PL2<-predict(ML2,newdata=data.frame(a=A))
summary(ML2)
lines(PL2~A,col="green",lwd=2)

ML3<-nls(h~aa*(a/(bb+a))^1.5,data=H,start=list(aa=26,bb=8))
PL3<-predict(ML3,newdata=data.frame(a=A))
summary(ML3)
lines(PL3~A,col="blue",lwd=2)

ML4<-nls(h~aa*(a/(bb+a))^3,data=H,start=list(aa=26,bb=8))
PL4<-predict(ML4,newdata=data.frame(a=A))
summary(ML4)
lines(PL4~A,col="magenta",lwd=2)

# Let's try to make a nice picture in png format
png("Fig8.png",width=1500,height=1000)  # Give file name and number of pixels 

par(mar=c(5,7,2,1)+0.1) # For shift graphics borders
plot(NULL,xlim=c(0,300),ylim=c(0,35),xlab="Age (years)",
     ylab="Height (m)",cex.axis=2,cex.lab=2)
grid()
with(H,points(jitter(a),jitter(h),pch=20))
lines(Pgam~A,col="red",lwd=2)
lines(PL2~A,col="green",lwd=2)
lines(PL3~A,col="blue",lwd=2)
lines(PL4~A,col="magenta",lwd=2)
# Add legend
legend("bottomright",c("Statistical","Levakovic with c=2",
                       "Levakovic with c=1.5","Levakovic with c=3"),
       col=c("red","green","blue","magenta"),lwd=2,cex=2)
dev.off() # Close the graphics file

Appendix II
 
Treeless area (Arengukl = A)

Appendix III
 
Development class S = under regeneration
Appendix IV
 
Development class N = young stands

Appendix V
 
Development class L = pole stands

Appendix VI
 
Development class K = middle age stands

Appendix VII
 
Development class V = prematured stands




Appendix VIII
 
Development class Y = Matured stands
Appendix IX
 
Appendix X

Appendix XI
 
