In progress..

## The Famous Titanic Study

<br>

<p align="center"><img width=100% src=https://user-images.githubusercontent.com/44467789/66575859-4e214080-eb94-11e9-903b-891e94663b25.gif>
                                              Source: National Geographic Channel


<br>

## How To Use The Project 

<details>

<summary><b>Expand For Steps</b></summary>

<br>

__Step 1:__ [Install R Studio](https://www.rstudio.com/products/rstudio/download/#download)

__Step 2:__ Download the Titanic [Dataset](https://www.kaggle.com/pavlofesenko/titanic-extended)

</details>

<br>

## Table of Content 

- [Objective](#objective)
- [Approach](#approach)
- [Data Cleaning and Edit](#data-cleaning-and-edit)
- [Exploratery Data Analysis](#exploratery-data-analysis)
- [Data Analysis on Tableau](#data-analysis-on-tableau)



<br>

### Objective

Objective of the study is to predict the survival of passenger from the Titanic ship, with the use of Machine Learning algorithms. For accuracy, use ensemble techniques for prediction. For an extention of the project, one can insert the personal demographic data and check whether they would had survied the Titanic accident or not. 

### Approach

- Collect the data from kaggle - [Link](https://www.kaggle.com/pavlofesenko/titanic-extended)
- Edit the Original Dataset and Create the dataset for the study - [TitanicNew.csv](https://github.com/RutvijBhutaiya/The-Famous-Titanic-Study/blob/master/TitanicNew.csv) 
- Exploratery Data Analysis
-

<br>

### Data Cleaning and Edit

1.	We downloaded dataset from [Kaggle](https://www.kaggle.com/pavlofesenko/titanic-extended). The dataset is already extended – Kaggle + Wikipedia.

2.	In dataset we decided to consider Wiki_Age  and not Age – because of missing values in Age variable. 

3.	Even in duplicated variables like Boarded and Embarked, we choose Boarded due to the places full form names. 

4.	For simplicity - we made changes in Destination, and added new variable called DestinationCountry. DestinationCountry indicates only the country name unlike Destination with more details lie State and City. 

5.	From the original dataset we have also added one more variable called NameLength. This variable indicates length characters of the name. Before applying the logic we had also removed the double name checks in the variables like e.g. Nasser, Mrs. Nicholas (Adele Achem) become Nasser, Mrs. Nicholas. 

6. Lifeboat Support - we assume that the box with missing value under variable Lifeboat means particular passenger didn't received the support from the Lifeboat. And hence, we created new variable LifeboatSuppot - Yes / No. 

And at last after doing all these changes in the original dataset we created TitanicNew dataset for the prediction of the passenger survival study. 

<br>

### Exploratery Data Analysis

After setting up the working directory we in Exploratory Data Analysis we begun with treating missing value in the date.

```
## Treating Missing Values

colSums(is.na(tt))

missingfare = subset(tt, is.na(Fare))

missingage = subset(tt, is.na(Age_wiki))
```

1.     Missing Fare value treatment: Wechecked – Passengers Demographics (Boarded, PClass, Sex, Destination Country)and then done analysis in Tabelue with respect to demographics and set theAverage missing passenger Fare. [Checked Tabelus Pic missingfare]

<p align="center"><img width=78% src=https://user-images.githubusercontent.com/44467789/66712011-e8130400-edb3-11e9-85fd-8298c91e45d8.png>
 
 <br>


2.     Missing value Age: We checkedpassenger Demographics (SibSpouse & ParentChild) based on which we tried toaverage down the missing vale in Age, However, we found it’s similar toActual Mean of Age_wiki. Hence we took that means only.

```
##* See the MissingFare Analysis on Tabelue and Selected Avg. = 13.4
##* See the MissinfAge Analysis on Tabelue and Select Avg. 
##* Age_wiki Avg.: 29.42 and Age_Months: 351


tt$Fare[is.na(tt$Fare)] = '13.4'

tt$Age_wiki[is.na(tt$Age_wiki)] = '29.42'

tt$Age_Months[is.na(tt$Age_Months)] = '351'

##* Fare, Age_wiki & Age_Months converted to Character
##* Convert back to Integer & Numeric

tt$Fare = as.integer(tt$Fare)
tt$Age_wiki = as.numeric(tt$Age_wiki)
tt$Age_Months = as.numeric(tt$Age_Months)
```

And the Ratio from the  dataset for Survived and Not Survived passenger is 0: 61.6 and 1: 38.3

```

## Ratio : Survived 1 and 0

as.matrix((prop.table(table(Survived)))*100)

# [,1]
# 0 61.61616
# 1 38.38384

```

<br>

#### Data Analysis on Tableau 

Before we jump on our machine learning modeling we studied variables and data analysis on the titanic dataset with the help of Tableau.  

##### 1. Passenger Class Survived Ratio

<p align="center"><img width=78% src=https://user-images.githubusercontent.com/44467789/66712145-024de180-edb6-11e9-8b56-37ab867d036e.png>
<br>
  
Pie chartshows, Passenger Class wise survived passenger ratio. This clearly indicatedmore than half of the passengers survived the Titanic accident was fromPassenger Class 1, and lease passenger were survived were from Class 3. Thisclearly indicated that even though the Class 1 passenger was less on countthey got the higher priority and hence their survival ratio is 63%.

<br>

##### 2. Passenger Hometown

<p align="center"><img width=88% src=https://user-images.githubusercontent.com/44467789/66712169-49d46d80-edb6-11e9-9925-2a35ed564dd1.png>

<br>

PassengerHometown geography map indicated that % ratio of total passengers from different- different country locations. Majority of the passengers were from the UnitedKingdom and The United States with 23.6% and 21.77% respectively. 

<br>

##### 3. Passenger Boarded and Survived –Gender wise

<p align="center"><img width=88% src=https://user-images.githubusercontent.com/44467789/66712190-899b5500-edb6-11e9-9cfa-e19df0085fda.png>
  
<br>

Passenger Boarded and Survived – Gender wise barchart indicate the ratio of Male and Female passenger class with respect tothe port they boarded. This bar chart indicate that the majority of thepassengers boarded the Titanic ship from the port of Southampton. However, thepassenger who didn’t survive the crash was also from the same group of the cluster – 40.04%. This is mainly due to Pclass – passenger class. Class 3passenger count is substation high compare to Class 1 passenger and Class 3passenger was boarded from the port of Southampton. But, unfortunately only24% of passengers from Class 3 passengers cluster were survived and the rest 76% werenot lucky. From the chart, we can also observe that all the male passengers boardedfrom Belfast were not lucky to survive the crash. 

<br>

##### 4. Passenger Survived – Age wise

<p align="center"><img width=58% src=https://user-images.githubusercontent.com/44467789/66712211-d8e18580-edb6-11e9-87aa-1978b520a966.png>

<br>

Passengersurvived – Age-wise classification is shown in the Box Plot.  This box plot indicates that the average ageof female passenger, survived the Titanic accident was 29 Years. And theaverage age of a female passenger did not survive was 24.2 Years.  In male passenger case the situation reverses,the average age of male passengers, did not survive was 30.8 Years. And theaverage age of male passengers, survived was 27.2 Years. This indicates the elderfemale class and young male class had high survival ratio than the younger femaleclass and elder male class.

<br>

##### 5. Passenger Class wise Fare / LifeboatSupport

 <p align="center"><img width=74% src=https://user-images.githubusercontent.com/44467789/66712260-8a80b680-edb7-11e9-9968-ceadb077eb16.png>
  
<br>
In this bar the chart we can see that the % Ratio of Fare is obviously higher for Class 1passengers. But, when we analyze - was their discrimination for lower classpassengers! This chart clearly indicated that 1st Class passengersgot priority in Lifeboat due to their high paid tickets. When we compare theLifeboatSupport with % of Fare Average – we observed that ticket Fare price averageis not very high for passengers who received the Lifeboat support. This ismainly due to the Class 1 passengers. However, due respect to the count of Class 3passengers and their low ticket value they did not luck to access Lifeboat onpriority.

<br>

##### 6. Parents Children – Spouse Siblings

<p align="center"><img width=62% src=https://user-images.githubusercontent.com/44467789/66712272-ce73bb80-edb7-11e9-87b2-7ce314c391b8.png>

<br>

ParentsChildren and Spouse Siblings bar chart indicated that solo passenger withoutParents or Children’s family members’ survival is high. Similarly, a passenger who has not traveled with Spouse or Siblings also had a high survival ratio.

<br>
                       
#### Outlier Study

We began the Outliers study with the Fare variable. In the Outliersidentification  we did the study on Fare,SibSpouse , ParentsChild, Age_Month, NameLength variables. 

- Remove Less Logical Fare observation ??
- 1. 0 Fare : Remove 
- 2. $5 : 1Class passenger : Remove [Erroe : $5 passengertraveling in 1st class!]
- 3. $69.55 : 3Class passenger : 11 passengers :Remove.[Person pay high tkt and travel in 3 class!]
- 4. $56.49 : 3Class passenger : 8 passengers :Remove.[Person pay high tkt and travel in 3 class!] 

```
boxplot(Fare ~ Pclass, data = tt, 
        main = 'Fare with respect to Passenger Class', ylab = 'Price', col = 'darksalmon')
```

<p align="center"><img width=80% src=https://user-images.githubusercontent.com/44467789/66922134-16a70e00-f044-11e9-8baf-0fcc1be5f6f5.png>
  
However, we decided not to remove the Outliers from the Fare feature, because it's logical, that 1st class passenger paid high Fare. So we decided not to remove the outliers from the Fare feature. 

For SibSpouse and ParentsChild feature, we found close outliers. Hence, we decided to do the Hypotheses testing to know the significant impact on the Target variable. 

For the following 2 features, we did hypothesis testing after removing the outliers from the features. And checked the p-value. 

```
## Boxplot Analysis for Outliers!

par(mfrow = c(1,2))

boxplot(SibSpouse ~ Survived, data = tt, 
        main = 'Sibbling / Spouce with respect to Survived', ylab = 'Count', col = 'darksalmon')

boxplot(ParentsChild ~ Survived, data = tt, 
        main = 'Parents / Children with respect to Survived', ylab = 'Count', col = 'darksalmon')
```

<p align="center"><img width=80% src=https://user-images.githubusercontent.com/44467789/66922688-2d019980-f045-11e9-95c1-1078b4a54fc2.png>

- NOTE: 1. Remove Outliers from SibSpouse & ParentChild
- NOTE: 2. Chk the Correlation on dependent variable 
- NOTE: 3. Hypothesis Test

```
# SibSpouse Feature

SibSpouse1 = subset(tt, SibSpouse <= 4)

cor(SibSpouse1$SibSpouse, SibSpouse1$Survived)

t.test(tt$SibSpouse, SibSpouse1$SibSpouse)

# p-value = 0.04271 # Hence, Reject Null Hypo (95% Confidence)- Significant Diff. # Remove Outliers

# %%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%

# ParentsChild Feature

ParentsChild1 = subset(tt, ParentsChild <= 2)

cor(ParentsChild1$ParentsChild, ParentsChild1$Survived)

t.test(tt$ParentsChild, ParentsChild1$ParentsChild)

# p-value = 0.009444 # Hence, Reject Null Hypo (95% Confidence)- Significant Diff. # Remove Outliers

# Hence, removed the Outliers from SibSpouse and ParentsChild variables

tt = tt[which(tt$SibSpouse <= 4 & tt$ParentsChild <=2),]

```

Hence, based on p-value we decided not to remove the outliers. 


Other Features - Age_Months & NameLength Outliers Study

```
boxplot(Age_Months ~ Survived, data = tt, 
        main = 'Age in Months with respect to Survived', ylab = 'Age Months', col = 'darksalmon')

boxplot(NameLength ~ Survived, data = tt, 
        main = 'Name Length of Male/Female Passengers', ylab = 'Name Length', col = 'darksalmon')
```

<p align="center"><img width=80% src=https://user-images.githubusercontent.com/44467789/66923222-0a23b500-f046-11e9-8534-4fcb3f70b54e.png>
  
There are few Outliers (Not very large) in the tt dataset, But for significant purpose we decided to consider it in the stud for Age_Month and NameLength. 

#### Correlation Study between features 

```
## Coorelation 

ggcorrplot(cor(tt[, c(2,3,5,7,8,10,12)]), method = 'circle',  type = 'lower', lab = TRUE)
```
<p align="center"><img width=88% src=https://user-images.githubusercontent.com/44467789/67010275-f3936180-f10a-11e9-9b22-ec11ccec0a0b.png>

As we can see in the correlation chart, PClass and Fare have the highest negative correlation, along with the target variable. Before building the Machine Learning models we will also do the feature selection through the Boruta package in R. 


#### Normalization Feature - Skewness

Based on the Histogram study, we decided to study normalization for continious variables. We used BoxCox.Lambda test to normalize the data. 

Based on the histogram, we found that Age_Months and NameLengths are normally distributed. But, Fare is right skewed. 

```
library(forecast)

hist(Age_Months, col = 'salmon')
BoxCox.lambda(Age_Months)
# [1] 0.5972085

hist(NameLength, col = 'Salmon')

hist(Fare, col = 'Salmon')
BoxCox.lambda(Fare)
```
<p align="center"><img width=80% src=https://user-images.githubusercontent.com/44467789/67006267-559b9900-f102-11e9-9618-5be63d8ea79d.png>
  
As we can see in the histogram Fare is right skewed and hence, we use log() for normalization. 

```
tt$Fare_new = log(tt$Fare)
# [1] 4.102259e-05 BoxCox Test

# Remove Fare and Keep Fare_new
tt = tt[, -c(10)]

# Also Remove Age_Wiki, IN study forward we'll consider Age_Months
tt = tt[, -c(11)]

write.csv(tt, 'TitanicCleanData.csv')
```
Save the clean dataset into new file for the machine learning modeling - [TitanicCleanData.csv](https://github.com/RutvijBhutaiya/The-Famous-Titanic-Study/blob/master/TitanicCleanData.csv)









