# MIMICIII-Investigation
A probe into the MIMIC III dataset. 

## Goal:
The goal of this project is to probe some basic information from the MIMIC III dataset. 
## The data:
MIMIC-III (Medical Information Mart for Intensive Care III) is a large, freely-available database comprising deidentified health-related data associated with over forty thousand patients who stayed in critical care units of the Beth Israel Deaconess Medical Center between 2001 and 2012.

The database includes information such as demographics, vital sign measurements made at the bedside (~1 data point per hour), laboratory test results, procedures, medications, caregiver notes, imaging reports, and mortality (both in and out of hospital).

MIMIC supports a diverse range of analytic studies spanning epidemiology, clinical decision-rule improvement, and electronic tool development. It is notable for three factors:

* it is freely available to researchers worldwide
* it encompasses a diverse and very large population of ICU patients
* it contains high temporal resolution data including lab results, electronic documentation, and bedside monitor trends and waveforms.



Citation: https://mimic.physionet.org/about/mimic/ 

## Detail:
For a more detailed description of the proposal please see the .tex file or .pdf file.
The goal of this project is to predict the survivability of patients based off of demographic information along with speed of treatment, type of infection, type of antimicrobial treatment, as well as other drugs and vital information. While sepsis is well studied, it is still partially responsible for ~6% of all deaths in the United States. More information and a better understanding of tailoring individual treatments for patients may improve its survivability.
Once input into a Postgres database, there are 20 tables with patient information and 5 dictio- nary lookup tables. Much of the data is dicult to process due to lack of standardization across multiple source databases(CareVue and MetaVision). Most of the useful information with date-time
information associated with it is available in the following tables:

- [x] **Admssions**
Contains information related to a patient's admission. This information includes their hospital stay id, insurance type, date of admission, and suspected diagnosis/con-
dition. An example is provided below. This snapshot of the table has not been manipulated in any way other than selecting patients admitted with sepsis.
<img width="500" src="./Data Visualizations/admission - Copy.png" alt="logo" />
 
 
 - [x] **patients:**
Patient information such as date of birth, gender, hospital stay id, etc. An example is provided below. Again, this table has not been manipulated in any way other than selecting  patients that were admitted with sepsis.
<img width="700" src="./Data Visualizations/patients.png" alt="logo" />
    
 - [x] **labevents:**
 Patient lab events with date-time associated with the measurement. This includes information such as creatinine levels. This is a snapshot is an example of the layout of the
database prior to any reading and pre-processing.
 <img width="500" src="./Data Visualizations/vitals.png" alt="logo" />
 
 - [x] **microbiologyevents:**
 Patient microbiology tests with date-time associated. This includes tests for infections and resulting prescription. This snapshot below shows how the database is layed out prior to any pre-processing.
 <img width="700" src="./Data Visualizations/microbiology.png" alt="logo" />
 
### **Feature Selection**
There are many features that may be of little use when predicting the survivability of sepsis. The
more irrelevant features that exist, the more data is required to ensure they do not t to noise in
those features. It is important to remove the features that are of little use. Feature correlation was calculated and it was observed that the infection type was of little
correlation to the survivability of sepsis. The existence of any infection was of little use in predicting survivability as well, therefore these features were dropped from the dataset. With the remaining features, a random forest was trained and the resulting feature importances graphed in figure. As can be see below gender, insurance type, and admission type are of little use when predicting survivability. For most algorithms, this data will be dropped. For the neural network, it may be included since more complex relationships could be developed between the features.
 <img width="700" src="./Data Visualizations/feature_correlation - Copy.png" alt="logo" />
  
  The important features have been discov- ered and now machine learning models can be  trained on this cleaned and standardized data.
 <img width="700" src="./Data Visualizations/features.PNG" alt="logo" />
## Learn More:
To gain access to this dataset for your own project visit: https://mimic.physionet.org

**A short course is required to gain permission to the dataset.**
## Citations:
MIMIC-III, a freely accessible critical care database. Johnson AEW, Pollard TJ, Shen L, Lehman L, Feng M, Ghassemi M, Moody B, Szolovits P, Celi LA, and Mark RG. Scientific Data (2016). DOI: 10.1038/sdata.2016.35. Available from: http://www.nature.com/articles/sdata201635

Goldberger AL, Amaral LAN, Glass L, Hausdorff JM, Ivanov PCh, Mark RG, Mietus JE, Moody GB, Peng C-K, Stanley HE. PhysioBank, PhysioToolkit, and PhysioNet: Components of a New Research Resource for Complex Physiologic Signals. Circulation 101(23):e215-e220 [Circulation Electronic Pages; http://circ.ahajournals.org/content/101/23/e215.full]; 2000 (June 13).
