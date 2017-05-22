# DH-Homework

## Introduction & Summary
This report contains an exploratory analysis of hospital characteristics and their ratings, using scores from the Hospital Consumer Assessment of Healthcare Providers and Systems (HCAHPS). Specifically, this report looks at attributes of hospitals that clients care most about, and it also focuses on the relationship between a hospital's participation in the Value-Based Purchasing (VBP) program and the quality of care they provide, as defined by the dimensions provided in the HCAHPS. VBP programs create incentives for more client-centered care through value-based incentive payments that depend partially on the quality of the patient's experience. 

A direct comparison using 2017 scores between hospitals participating in a VBP program and hospitals that are not, shows that VBP Hospitals are comparatively worse. However, further analysis shows that participation in a VBP program has ambiguous if not negligible affects on hospitals' scores. 

Through regression analysis, one of the most important factors in a patient's overall score of a hospital, aside from communication from nurses, is the quality of their care transition. Interestingly, care transition is also the second lowest rated dimension on average. This shows that one of the most significant determinant in a client's perception of the hospital is also an area where healthcare is falling short, according to the patients.

The following sections include an overview of the data, the methodology and results, and a brief conclusion and discussion.

## The Data
The HCAHPS is the first national, standardized, publicly reported survey that focuses on the patient's perspective of  hospital care. An important feature of this data set is it's *linear mean scores*. The linear mean scores are a composite score that takes into consideration patient demographics and  (education, income, age, etc.) - the reason being that some demographics may have a tendency to rate hospitals a certain way. Because this score adjusts for the types of survey participants it is a less biased metric and allows for more objectful and meaningful comparisons across hospitals.

The linear mean score metrics are the following:
1. Care Transitions
2. Cleanliness
3. Communication, Doctor
4. Communication, Medicine
5. Communication, Nurse
6. Discharge Information
7. Pain Management
8. Quietness
9. Responsiveness of Staff
10. Overall Score

The 2015 and 2017 HCAHPS surveys are used in this study, along with the 2015 and 2017 HVBP datasets. 

## Methodology and Results (pt. 1: VBP vs Non-VBP)
The HCAHPS and HVBP datasets were combined and reshaped to contain two rows for each hospital - one with details in 2015 and one in 2017. It was trimmed to contain just the hospital ID, name, state, county, the 10 linear mean score metrics, and if the hospital was in a VBP program during that year. 

The first investigation uses the 2017 data and examines the differences between VBP hospitals and Non-VBP hospitals, shown in Table 1 below. In every metric, VBP hospitals had a lower average score than non-VBP hospitals. 

__Table 1: VBP vs Non-VBP Hospitals__

Metric|VBP Hospitals|Non-VBP Hospitals|Difference (VBP - Non-VBP)
---------|----------|----------|----------
Staff Responsiveness |	84.75 |	88.69 |	-3.94
Communication, Medicine	|78.33|	81.68|-3.35
Clean	|86.91	|90.03	|-3.12
Quiet	|82.65	|85.72	|-3.07
Communication, Doctor	|91.60	|93.37	|-1.77
Overall	|88.59|	90.25|	-1.66
Communication, Nurse	|91.17	|92.80|	-1.63
Discharge Info |	86.90|	88.52|	-1.61
Pain Management |	87.31|	88.91|	-1.61
Care Transition |	81.23	|82.82|	-1.59

This raises a classic issue of causality -- does being a hospital in a VBP program cause the hospital to have lower scores, or is there something else to the seemingly apparent relationship? This is explored below in Table 2, which looks solely at hospitals that were not enrolled in a VBP program in 2015, but were enrolled in 2017 (n = 86). The table shows the difference between these hospitals average 2017 scores and their average 2015 scores. There does not appear to be any significant changes between the two years.

__Table 2: "Newly VBP" Hospitals, 2015 & 2017 Rating Differences__

Metric|2015|2017|Difference (2017 - 2015)
---------|----------|----------|----------
Communication, Medicine|	79.90|	78.32|	-1.58
Care Transition 	|82.23	|82.40	|0.17
Discharge Info|	86.54	|85.80|	-0.74
Quiet|	86.05|	86.84|	0.79
Staff Responsiveness	|86.62|	87.32	|0.70
Clean|	88.46|	87.96|	-0.50
Pain Management|	88.21	|88.76|	0.55
Overall|	89.82|	90.12|	0.30
Communication, Nurse	|91.97	|92.08	|0.11
Communication, Doctor	|92.67	|93.60	|0.93

This suggests that the VBP program *does not* cause the hospital to have lower scores. The opposite scenerio is shown in Table 3 below, and looks at hospitals that were enrolled in a VBP program in 2015, but were not enrolled in 2017 (n = 257). Their 2015 and 2017 scores are shown, and, similarly, there does not seem to be any significant differences between 2015 and 2017. 


__Table 3: "Newly Non-VBP" Hospitals, 2015 & 2017 Rating Differences__

Metric|2015|2017|Difference (2017 - 2015)
---------|----------|----------|----------
Communication, Medicine|	78.62	|79.55	|0.93
Care Transition|	80.76|	81.10|	0.34
Quiet	|84.76	|85.08	|0.32
Staff Responsiveness|	85.86|	85.98|	0.12
Discharge Info	|86.20|	84.72	|-1.48
Clean	|87.38	|87.44|	0.06
Pain Management|	87.58	|87.56	|-0.02
Overall|	88.02	|88.04	|0.02
Communication, Nurse	|91.06	|91.12	|0.06
Communication, Doctor	|91.76	|92.53	|0.77

If being in the VBP program isn't causing the hospitals to have worse services, then there is likely to be another unobserved factor that's driving these differences. The VBP program likely attracts a certain type of hospital, for reasons that are exogenous to this data set, and this selection into the VBP program might explain these observed differences. 

## Methodology and Results (pt. 2: determinants of overall score)
In this section, I look at what determines the overall score for the hospital. To do this, I examine how the different scoring dimensions affect how the patient rates the hospital overall using the 2017 data. Because the overall rating is a separate question, rather than a construction from other questions, we can see which of the aspects affects the patient's view of the overall score the most. This is estimated by the regression equation, below.

![regression1](https://cloud.githubusercontent.com/assets/25534898/26292892/a85a6afc-3e87-11e7-97a3-6dccaa1a7b34.png)

The state binary variables control for any time-invariant characteristics of the state, while the array of linear mean score dimensions contains all nine ratings. The outcome of this regression is displayed below, with the different ratings on the y-axis, their respective bars corresponding to their beta coefficient, and their shade indicating their statistical significance (lighter shades are more statistically significant). 

![figure1](https://cloud.githubusercontent.com/assets/25534898/26292740/71c03d24-3e86-11e7-9ef1-41fa9013ea01.png)

The interpretation of this regression is that for every increase in 1 of the linear mean score of a dimension, it will increase the overall score of the hospital by that dimension's corresponding beta coefficient. E.g., an increase of 1 point in Care Transition increases the overall hospital rating by a little bit more than 0.3. 

This is interesting in that it's clear that patients value some aspects of the hospital more than others, and satisfaction in certain categories will increase their overall perception of the hospital more. The two standouts are communication with nurses and transition in care.

## Conclusion and Discussion

There are three main take-aways I had from this 
