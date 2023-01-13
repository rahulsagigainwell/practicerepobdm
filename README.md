# Introduction
Take the BDM legacy code and port it to Databricks. Listed below is a quick primer of BDM, the steps that will be taken to port over the legacy code to Databricks, and future goals.

# What Is BDM
BDM is an acronym for Big Data Matching. It is a process of a faster, more efficient way of performing Entity Resolution on a large set of data. The purpose of this is to take the members from NED(Commercial Insurance) and INDV(Medicaid) data and perform a process of matching these members with preestablished block rules based on various input fields such as SSN, first name, DOB, last name, etc. With these block rules, the primary provider can be determined for each member based on the similarity score that is derived from matching each id in these two datasets. 

# BDM Architecture
![BDMDataFlow](https://user-images.githubusercontent.com/109543462/212356725-c461832a-b783-43e2-a34f-c9b402627d4f.PNG)

# Block Key Rules
![BlockKeys](https://user-images.githubusercontent.com/109543462/212356863-3a37875f-0e67-4fa0-9b0a-081f2f79baf8.PNG)

# Short Description of Each Stage of BDM Process
* Data Stage: Input CDC and Master Tables, perform general data partitioning, and create function that incrementally updates the data given real time stream from the input tables
* Data Prep: Clean data in preparation for block matching and generate the 6 block keys. Final output are the NED_Prep and INDV_Prep tables
* Block/Match: Establish the 6 block rules and use these block rules to generate potential matching records from these two tables. Generate feature score for predicative analysis.
* Clustering/Cluster Pairs: Derive cluster matches and create cluster pairs 
* Cluster Features: Each cluster pair is given a score. The ones that are determined to be a perfect match as per a preexisitng Information System(iMatch) are verified. If not, these cluster pairs will enter the cluster resolve process
* Cluster Resolve: Fine tuning the feature scores for any fuzzy scores and invalid matches. If the score is high enough, these cluster pairs are verified. 
* Reformat iMatch: Reformat iMatch

# Current Goals
The current goal is to create a Shingling function and a Locality Sensitive Hashing Function with dummy data during the data prep stage while generating the 6 block keys in preparation for the block/match stage

## What Is Shingling?
Shingling is the method of tokenizing text according to the characters of the text. The most popular group of shingling will be in grams of two or three characters. For every shngle that occurs, one-hot encoding will set the position of that vector as 1. 

## What Is Locality Sensitive Hashing?
The next step in the process in MinHashing, which takes the sparse vector derived from shingling and converts into a dense vector. These dense vectors are then input into the Locality Sensitive Hashing algorithm. Unlike other hashing algorithms, LSH seeks to maximize conflicts between the inputted vectors to create candidate pairs. This is especially beneficial for large sets of data as the greater number of collisions result in candiate pairs being identified in a more efficient manner. 

# Future Goals
To create a working and functional POC of the BDM process on Databricks
