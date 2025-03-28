# A Draft Outline for Reproduction Analysis Report

## Key Contributions

1. Enhancing reproducibility through a reproduction study by developing a 4.5-star research compendium
1. Assessing internal validity and credibility of influential original research
   - https://osf.io/sma6g

## Introduction


**1. Establish the concept of reproduction and the purpose of doing reproduction analysis**

Doing reproduction analysis will allow other researchers to review, extend, and modify the study and will allow students of geography and spatial epidemiology to learn from the study design and methods.

**2. Introduce the topic of interest (people with disability, social inequity under public health crisis)**

Measuring the relationship between COVID-19 incidence and socio-demographic and disability characteristics can provide important information for public health policymaking and resource allocation.

**3. Introduce the original study**

Chakraborty (2021) investigates the relationships between COVID-19 rates and demographic characteristics of people with disabilities by county in the lower 48 states. His study aims to examine public concern that persons with disabilities (PwDs) face disproportionate challenges due to COVID-19. In particular, he aims to determine whether COVID-19 incidence is significantly greater in counties containing higher percentages of socio-demographically disadvantaged [people with disabilities], based on their race, ethnicity, poverty status, age, and biological sex

To investigate this, Chakraborty examines the statistical relationship between confirmed county-level COVID-19 case rates and county-level socio-demographic and disability variables. Specifically, Chakraborty tests county-level bivariate correlations between COVID-19 incidence against the percentage of disability and socio-demographic category, with a separate hypothesis and model for each subcategory within disability, race, ethnicity, age, and biological sex. To control for differences between states and geographic clusters of COVID-19 outbreaks, Chakraborty uses five generalized estimating equation (GEE) models to predict the relationship and significance between COVID-19 incidence and disability subgroups within each socio-demographic category while considering inter-county spatial clusters.

The study reveals significant positive relationships between COVID-19 rates and socially vulnerable demographic categories of race, ethnicity, poverty, age, and biological sex.

**4. Relevance of reproducing Jay’s paper**

- **Other research has already referenced this paper in subsequent studies.** Chakraborty’s paper has been referenced in 14 subsequent studies since its publication. Most of these studies continue to examine how people with disabilities (PwDs) have been adversely impacted by the COVID-19 pandemic in terms of their physical and mental health as well as access to food and medical resources (references). Other studies have developed on Chakraborty’s conclusion and investigate ways to mitigate and prevent adverse impacts of future pandemics on PwDs (references) or applied the method and conceptualization of Chakraborty’s study to different parts of the world (references).  

- **Disability is still important in the context of COVID-19 impacts.** Since the inception of the pandemic, there are 77 publications on the Disability and Health Journal, ranging from research articles, short communications to discussion and review articles that examine disability within the context of COVID-19. However, we found that only 33 of them published supplementary materials along with the paper. Among the 33 publications, only 7 provide accessible raw data, 3 provide instructions on raw data. 8 publications provide accessible processed data or intermediaries, and 10 publications provide other forms of accessible supplementary materials, such as survey instruments and interview guides.

- **Jay’s study is not computationally reproducible. The GitHub repository we created that include data, code, and metadata helps to confirm validity of study with significance for public health.** Few studies provide both raw data and intermediaries that allow others to reproduce the study and then check for its validity. However, none of the 33 publications with supplementary materials have provided code or repositories, creating barriers for doing reproduction analysis. Some of the supplementary materials provide information on the variables used in the study that serve as metadata of some kind, but they are not documented following the international standard. Similarly, Chakraborty did not publish any supplementary materials with this paper. Therefore, transforming it into a reproducible study by publishing a compendium complete with metadata, data, and code will increase its accessibility, transparency, and potential impact

**5. Introduce our reproduction study**

In this reproduction study, we attempt to implement the original study as closely as possible. Our reproduction study is organized into three parts. In part one, we aim to recreate the map of the county level distribution of COVID-19 incidence rates. In part two, we aim to reproduce the summary statistics for disability and sociodemographic variables and bivariate correlations with county-level COVID-19 incidence rate. Eventually, we aim to run the GEE model for predicting COVID-19 county-level incidence rate controlling for clusters in part three.

Our two confirmatory hypotheses are that we will be able to exactly reproduce Chakraborty's results as presented in figure 1, table 1, and table 2 of Chakraborty (2021). Stated as null hypotheses:

> H1: There is a less than perfect match between Chakraborty's bivariate correlation coefficient for each disability/sociodemographic variable and COVID-19 incidence rate and our bivariate correlation coefficient for each disability/sociodemographic variable and COVID-19 incidence rate.

> H2: There is a less than perfect match between Chakraborty's beta coefficient for the GEE of each disability/sociodemographic variable and our beta coefficient for the GEE of each disability/sociodemographic variable.

## Methods

### Software

The original study was conducted using ArcGIS (Desktop v 10.7), SPSS, and SaTScan (v9.6). The SaTScan software was used to implement the spatial scan statistics. ArcGIS was used to conduct spatial analysis and mapping. Other statistics were calculated in SPSS.

To make this study reproducible, we have implemented the analysis to the greatest extent possible in R/RStudio. We used the SpatialEpi package to implement spatial scan statistics, the tmap and sf packages for mapping and spatial analysis, the geepack as well as the tidycensus packages for the generalized estimating equation and data extraction.

- The geepack implements the generalized estimating equations approach for fitting marginal generalized linear models to clustered data, mostly found in longitudinal data and repeated measures. The GEE approach focuses on models for the mean of the correlated observations within clusters without fully specifying the joint distribution of the observations (Højsgaard et al. 2005).

- The SpatialEpi package implements methods for spatial epidemiology that includes disease mapping, spatial regression/geographic correlation studies, and analysis of disease clusters. The basis of this model is to partition a study region into a set of areas which are either null or non-null, the latter corresponding to clusters or anti-cluster (Kim & Wakefield 2010).

- The tmap package offers a coherent plotting system for thematic maps that is based on the layered grammar of graphics (Tennekes 2018).

- The sf package is an R package for reading, writing, handling, and manipulating simple features in R (Pebesma 2018).

- The tidycensus package is an R package designed to facilitate the process of acquiring and working with US Census Bureau population data in the R environment. It makes census data available to R users in a tidyverse-friendly format. It is also designed to streamline the data wrangling process for spatial census data analysts (Walker 2022).

- Comparing SpatialEpi and SaTScan: Kim, A. Y., & Wakefield, J. (2016). A Bayesian Method for Cluster Detection with Application to Brain and Breast Cancer in Puget Sound. Epidemiology (Cambridge, Mass.), 27(3), 347–355. [https://doi.org/10.1097/EDE.0000000000000450](https://doi.org/10.1097/EDE.0000000000000450)


### Measures

**1. Data sources**
The data on disability and sociodemographic characteristics come from the U.S. Census American Community Survey (ACS) five-year estimates for 2018 (2014-2018). This data is publicly available online and we downloaded it directly from the Census API using the tidycensus package for R. Chakraborty informed us of the ACS data table names used in the study (S1810 for demographic categories and disability status and C18130 for poverty status and disability status)

The COVID-19 data comes from the Johns Hopkins Coronavirus Resources Center and could be found at the John Hopkins CCSE COVID-19 Data Repository. This data expresses cumulative count of reported COVID-19 from 1/22/2020 (when John Hopkins began collecting the data) to 8/1/2020 (when the data was retrieved for the original study). Since it is not possible to download that dynamic dataset in an archived form as it existed on August 1, 2020, we have asked Chakraborty for this data.  

**2. Variables and their characteristics**

Both the COVID-19 data and the demographic data are measured at the county level in the 48 contiguous states in the US. The COVID-19 incidence rate is the dependent variable of this study. There are eighteen independent variables, a percentage of total disabled persons per county and seventeen 'disaggregated' categories that break down socio-demographic characteristics of the disabled population.

**3. Variable transformation**

For the first two parts of our reproduction analysis, the COVID-19 incidence rate is normalized at the county-level per 100,000 people. Most of the disability and sociodemographic variables are provided in the format that they are used, as a percentage of "people with disabilities in each subgroup by the total civilian non-institutionalized population relevant to the variable category" (Chakraborty 2011). Non-Hispanic non-White, Below poverty level and Above poverty level are calculated as shown in table above.

For the third part of our reproduction analysis, we have normalized all independent variables into z-scores. For the GEE, two different clustering scores are assigned to each county. The first clustering ID is a categorical variable determined by the counties' state. The second clustering ID is a relative risk score calculated by identifying spatial clusters from a spatial scan statistic based on the Poisson Model. WE calculated the clusters using the SpatialEpi package in R and then the relative risk score for each county using the formula: ``(rate of cases within the cluster) / (rate of cases outside the cluster)``. We classified the relative risk scores into six categories based on the estimated relative risk values (<1.0, 1.00-1.99, 2.00-2.99, 3.00-3.99, 4.00-4.99, and 5.0 or more). The first clustering ID (State) and second clustering score (Classified Relative Risk) were combined to form IDs for each unique combination of state and relative risk class. The clustering ID's were joined with the ACS data on disability subgroups and used as input to the GEE models.

### Analyses
**1. Choropleth map**


**2. Descriptive statistics and bivariate analysis**


**3. GEE**


## Results
- Unplanned deviations in reproduction analysis
- Part 1 results
- Part 2 results
- Part 3 results

## Discussion
