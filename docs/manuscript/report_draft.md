# Complete Draft for Reproduction Analysis Report

**Need citation for highlighted sentences**

## 1. Introduction

The COVID-19 pandemic has exacerbated the problem of social inequity inherent in various aspects of people’s life across the country.
Since its inception, researchers have produced a deluge of studies that investigate how socio-demographically disadvantaged population have been adversely affected by the pandemic and have proposed solutions that address this acute inequity for government officials and policymakers to consult.

The study by Chakraborty exemplifies one of these attempts by researchers to understand social inequity in the context of COVID-19.
Chakraborty investigated the relationship between COVID-19 rates and demographic characteristics of people with disabilities by county in the lower 48 states.
**In particular, he aims to determine whether COVID-19 incidence is significantly greater in counties containing higher percentages of socio-demographically disadvantaged people with disabilities (PwD), based on their race, ethnicity, poverty status, age, and biological sex.**
The decision by Chakraborty to measure the association between COVID-19 incidence and disability characteristics was because the result could provide important implications for public health policymaking and resource allocation as well as for future research on spatial epidemiology.

Nevertheless, for policymakers to make informed and effective decisions, they must know not only the results of the studies, but also their reliability.
For other researchers to review, extend, and modify the studies, they must also know the process of which the author reached the conclusion and be able to access any supplementary materials.
Chakraborty’s study, however, lacks critical elements for policymakers to validate the result and for other researchers to learn the research design, which risk the potential to impair decision making and undermine the significance of original research.

One way to establish the credibility and transparency of research findings is by conducting reproduction analyses.
**A reproduction study aims to find the same results using the same data and methodology as a published study (NASEM, 2019).**
**Once a study is reproducible, it becomes possible to reanalyze the original study design by purposefully altering parameters or procedures using the same data (Christensen et al., 2019).**
**In addition, a reanalysis on the original study provides insight into the sensitivity of original results by testing the internal validity of the finding and demonstrating how the finding compares to a set of findings produced by possible alternative analyses (Holler & Kedron, 2022).**
While the significance of reproduction studies is widely recognized, there has been a dearth in literature that focuses on reproducing any studies and document the process, barriers, and outcomes of doing so.

We began to address this gap by reproducing the work of Chakraborty and completing a reproduction compendium with metadata, data, and code.
The overarching value of this reproduction study is that we will be able to enhance the credibility of the Chakraborty’s research by reducing potential uncertainties and determine if the results are robust enough for policymakers to make informed decisions.
Moreover, we will be able to understand the challenges of doing reproduction analyses, enhance their transparency, and evaluate the efficiency while making improvements to the research methods.

We select this particular study to reproduce for three reasons.
First, the condition of PwD continues to be an issue of concern in the context COVID-19.
Chakraborty has summarized several major challenges that PwDs have been facing.
**In particular, PwDs who rely on assistance with personal care need to adopt public health guidelines that do not often consider their needs.**
**PwDs often have difficulty communicating symptoms of illness and are more likely to be disadvantaged in terms of health care access.**
These issues continue to incentivize researchers to conduct further investigations.
Through searching for the keyword “COVID” in the Disability and Healthy Journal, we found that since 2020, there are 77 publications, including research articles, short communications, discussion, and review articles, that examine disability within the context of the pandemic.  

Second, Chakraborty’s study has been influential in the academia; it has been referenced in 19 subsequent studies since publication.
**Most of these studies continue to examine how PwDs have been adversely impacted by the pandemic in terms of their physical and mental health as well as access to food and medical resources.**
**Other studies have developed on Chakraborty’s conclusion and investigate ways to mitigate and prevent adverse impacts of future pandemics on PwDs or applied the method and conceptualization of Chakraborty’s study to different parts of the world.**

Third, Chakraborty’s original study was not computationally reproducible.
Therefore, transforming it into a reproducible study by publishing a compendium could increase its accessibility, transparency, and potential impact.
More importantly, among the 76 articles on COVID-19 and disability, we found only 40.7% of them have published some form of supplementary materials (8% provided raw data, 13.3% provided processed data, and 2.6% provided data access instructions and 21.3% provided survey instruments or interview guides).
Few studies have provided both the raw data and intermediaries that allow others to reproduce the study and check for validity.
Some of the supplementary materials provided information on the variables used in the study that serve as metadata of some kind, but they are not documented following the international standard.
Accordingly, our study will also add to the paucity of reproduction studies done in this field.

The paper is organized into five sections.
In the following section, we briefly introduce the research methods, results, and implications of Chakraborty’s study.
In the third section, we present our data sources, characteristics, the structure of our reproduction analyses, and how our approach deviates from that of the original.  
In the last section…

## 2. Statistical Analyses and Findings of Chakraborty (2021)

Chakraborty examined the statistical relationship between confirmed county-level COVID-19 case rates and county-level socio-demographic and disability variables.
Specifically, he first visualized the national distribution of COVID-19 incidence rate and computed summary statistics for COVID incidence and each socio-demographic variable.
He then tested county-level bivariate correlations between COVID-19 incidence against the percentage of disability and socio-demographic category using Pearson’s correlation coefficient, with a separate hypothesis and model for each subcategory within disability, race, ethnicity, age, and biological sex.
To control for differences between states and geographic clusters of COVID-19 outbreaks, Chakraborty used five generalized estimating equation (GEE) models to predict the relationship and significance between COVID-19 incidence and disability subgroups within each socio-demographic category while considering inter-county spatial clusters.
According to Chakraborty, GEEs extend the generalized linear model to accommodate clustered data, in addition to relaxing several assumptions of traditional regression.
Additionally, he noted that "clusters of observations must be defined based on the assumption that observations within a cluster are correlated while observations from different clusters are independent."
He used a combination of two different approaches to define county clusters: the state and the significant clusters of COVID-19 cases.
The latter approach is implemented with spatial scan statistics based on the Poisson model to determine spatial clusters and calculate relative risk (RR) for each county.
All five GEE models will be specified with exchangeable correlation matrices, gamma distributions, and logarithmic link function.
These specifications were chosen after testing each alternative and choosing the models with the best quasi-likelihood under the independence model criterion (QIC).

The original study was conducted using ArcGIS (Desktop v 10.7), SPSS, and SaTScan (v9.6).
The SaTScan software was used to implement the spatial scan statistics.
ArcGIS was used to conduct spatial analysis and mapping.
Other statistics were calculated in SPSS.

Chakraborty’s study reveals significant positive relationships between COVID-19 rates and socially vulnerable demographic categories of race, ethnicity, poverty, age, and biological sex.
The primary conclusions are that PwDs who are racial/ethnic minority, below poverty, aged 5-17 years, and female are significantly overrepresented in counties with higher COVID-19 incidence.

## 3. Data and Approach to Reproduction Analysis

### 3.1 Software

To make this study reproducible, we implemented the analysis to the greatest extent possible in R/RStudio.
We used the SpatialEpi package, which implements the methods for spatial epidemiology that includes disease mapping, spatial regression, and analysis of disease clusters, to computes spatial scan statistics.
**The basis of this model is to partition a study region into a set of areas which are either null or non-null, the latter corresponding to clusters or anti-cluster (Kim & Wakefield 2010).**
**The tmap and sf packages are used for mapping and spatial analysis: the former offers a coherent plotting system for thematic maps based on layered grammar of graphics (Tennekes 2018) and the latter is a handy tool for reading, writing, handling, and manipulating simple features in R (Pebesma 2018).**
The geepack package is used for the GEE model.
**This package implements GEE by fitting marginal generalized linear models to clustered data, mostly found in longitudinal data and repeated measures (Højsgaard et al. 2005).**

### 3.2 Data

The data on disability and sociodemographic characteristics comes from the U.S. Census American Community Survey (ACS) five-year estimates for 2018 (2014-2018). Chakraborty informed us of the ACS data table names used in the study (S1810 for demographic categories and disability status and C18130 for poverty status and disability status). Using this information, we obtained the data via the Census API using the tidycensus package for R. **This package is designed to facilitate the process of working with US Census Bureau population data in the R environment in a tidyverse-friendly format (Walker 2022).**

The COVID-19 data comes from the Johns Hopkins Coronavirus Resources Center and is available at the John Hopkins CCSE COVID-19 Data Repository. This data expresses cumulative count of reported COVID-19 from 1/22/2020 (when John Hopkins began collecting the data) to 8/1/2020 (when the data was retrieved for the original study). Since it is not possible to download that dynamic dataset in an archived form as it existed on August 1, 2020, we have asked Chakraborty for this data in order to be consistent with the original research.

Both the COVID-19 data and the demographic data are measured at the county level in the 48 contiguous states in the US. The COVID-19 incidence rate is the dependent variable of this study. There are eighteen independent variables, a percentage of total disabled persons per county and seventeen 'disaggregated' categories that break down socio-demographic characteristics of the disabled population.

### 3.3 Reproduction analysis of Chakraborty (2021)

Following the analytical framework of the original analysis, our reproduction study is organized into three parts.
In the first part, we recreate the map of the county level distribution of COVID-19 incidence rates.
In the second part, we reproduce the summary statistics for disability and sociodemographic variables and bivariate correlations with county-level COVID-19 incidence rate using Pearson’s correlation coefficient.
Eventually, we reproduce the GEE model for predicting COVID-19 county-level incidence rate controlling for clusters in third parts.
For each part of our analysis, we compare our results to the original results, accounting for differences in computational environment and analytical decisions.
The data, code, and metadata of this reproduction analysis are available at [https://osf.io/s5mtq/](https://osf.io/s5mtq/)

In the first two parts of our reproduction analysis, we found that one county was unexpectedly missing disability and poverty data and replaced it with zeroes.
We also recognized that most of the independent variables have non-normal distributions, and therefore we used the nonparametric Spearman's rank correlation coefficient for bivariate tests of correlation between the independent variables and COVID-19 incidence rates.
In order to better understand the geographic patterns underlying the correlations between disability and COVID-19, we also visualized disability rates by county.

In the third part of our reproduction analysis, we discovered that the original study most likely conceptualized COVID-19 clusters as the local relative risk of the county at the center of the cluster.
In other words, counties inside of a cluster but not at its center were excluded in the original study and assigned the lowest risk category.
Therefore, we changed our conceptualization of COVID-19 clusters to include all counties within any cluster.
We first calculated the local relative risk to investigate intra-cluster variations and created a map showing the relative risk score of each county.
Then, we created a list of cluster IDs from the SpatialEpi output in order to identify all counties within a cluster and classify their risk.
We calculated the relative risk score for each cluster and classified them on a scale from 1 to 6 and recalculated the generalized estimating equations using this alternative conceptualization of COVID-19 risk.

To better understand how the original research used the Kulldorff spatial scan statistic, we decided that additional data visualizations would improve our understanding of the spatial patterns and better illustrate the differences in results.
As such, we created maps visualizing the spatial clusters of COVID-19 incidence based on the output of SpatialEpi and SaTScan.

## 4. Results

The first part of our reproduction analysis was to visualize the spatial distribution of COVID-19 cases per 100,000 in the US (Figure).
The reproduction results closely resembled that of the original study.
In addition, we proceeded to create a map that illustrated the percentages of population with disability in each county (Figure).

The second part of our reproduction analysis focused on computing the summary statistics for variables analyzed and the bivariate correlations with county COVID-19 incidence rates.
Our summary statistics and Pearson's correlation coefficients were consistent with those of Chakraborty’s but differ slightly in magnitude.
Since the Pearson's correlation should only be used on variables with normal distribution, we calculated the Spearman's Rho correlation coefficient (Table).
There seems to be more changes to the result in terms of their magnitude and direction.
While the Pearson's correlation coefficient shows a weak positive relationship between "COVID-19 incidence rate" and "Percentages with disability that are Native American" and "Percentages with disability that are female", these turned into weak negative relationships in Spearman's correlation coefficient.

Although Chakraborty does not illustrate the classified relative risk of COVID-19 clusters, we enhanced the study by mapping both relative risk based on the SaTScan results (Figure) and on our R SpatialEpi results (Figure).
On top of that, we calculated and mapped the relative risk score for each cluster (Figure).

In the third part of our reproduction analysis, we implemented the GEE model (Table).
The results of our reproduction study are mostly consistent with that of from Chakraborty's, with slight differences in the magnitude of correlation coefficients. The significance of some of the results also changed: the percent of people with disability who fall into none of the racial group and percent of people with disability who are Hispanics changed from being significant to non-significant whereas the percentage of disabilities between 18-34 changed from being non-significant to significant.
