---
id: d4dd9201-c58d-4f4d-aa38-498c8c6e6267
title: Survival Analysis
desc: ''
updated: 1614537039741
created: 1605125570606
---
# Survival analysis
Survival analysis is a branch of **statistics** for analyzing the expected duration of time until one or more events happen, such as death in biological organisms and failure in mechanical systems. - [wikipedia](https://en.wikipedia.org/wiki/Survival_analysis)

Historically, originally developed and used by acturaries and medical researchers to estimate population lifetimes. 

- [Video: Censoring](https://www.youtube.com/watch?v=vX3l36ptrTU)
    ![](/assets/images/2020-11-11-15-12-53.png)
    - **Assume**: censoring is non-informative - being censored or not is not related to the probablity of event happening

- [Video: Survival Function, Hazard, & Hazard Ratio](https://www.youtube.com/watch?v=MdmWdIV5k-I)
    - **Survival function**: S(t) = P(T>t) = prob. of survival beyond time t
    - **Hazard**: HAZ = P(T< t + dt | T >t)
             = prob of dying in next few seconds, given alive now
    - **Hazard ratio** (HR)  , prob of dying in next few seconds given exposure vs. not 
    
        \\(  HR = {HAZ, x=1 \over HAZ, x=0} \\)
    
- [Video: comparing 3 ](https://www.youtube.com/watch?v=K7bmmbD7KIg)

    model | Kaplan-Meier | Exponential | Cox-PH model
    ------|--------------|------------|-------------
    type | non-parametric | parametric | semi-parametric
    prob | Simple <br>  can est S(t) | can est S(t) and HR | hazard can fluctuate with time <br> can est HR 
    con |  No functional form <br> cannot est HR * | not always realistic <br> assume constant HAZ <br> Weibull model allows haz to proprotially ↗ or ↘	with time) | cannot est S(t)

- [Video: part 4- Kaplan-Meier model](https://www.youtube.com/watch?v=VJPPeUpyC6c)
    - Process to compute the survival curve:
        ![](/assets/images/2020-11-11-16-25-29.png)
    - censored data get incorporated for all the prob. calculations before they drop out 
    - a tick indicate censored data 
    - example graph from [water pipe break paper](https://www.researchgate.net/publication/338223962_Improving_Urban_Water_Security_through_Pipe-Break_Prediction_Models_Machine_Learning_or_Survival_Analysis)
        ![](/assets/images/2020-11-11-16-29-36.png)
          

- [Video: Exponential Model](https://www.youtube.com/watch?v=T_goHnU8Eu4&list=PLqzoL9-eJTNDdnKvep_YHIwk2AMqHhuJ0&index=6)
  ![](/assets/images/2020-11-13-15-35-26.png)
  ![](/assets/images/2020-11-13-15-36-57.png)


- [Video: Exponential vs Weibull vs Cox Proportional Hazards](https://www.youtube.com/watch?v=KDpAtrqS39w&list=PLqzoL9-eJTNDdnKvep_YHIwk2AMqHhuJ0&index=7)
 
    - Overall:
        - \\( Survival Function = S(t) = P(T>t) = e^{-HAZ*t} \\)
        - \\( HAZ = e^{ b_{0} + b_{1}x_{1} + b_{2}x_{2} + ... +  b_{k}x_{k}} \\)
        - \\( \ln(HAZ) = b_{0} + b_{1}x_{1} + b_{2}x_{2} + ... +  b_{k}x_{k} \\)
        - \\( b_0 \\) is \\( \ln(HAZ) \\) for reference (at T=0)
    - **Exponential**
        - \\( b_0 \\) is constant -> constant hazard 
    - **Weibull**
        - \\( b_0 \\) is proprotional to time:  \\( \ln(\alpha) \ln(t) + b_0 \\) =>  \\( b_0 \\) 
        -  \\(\alpha = 1 \\) - constant hazard
        -  \\(\alpha > 1 \\) -  hazard increase with time
        -  \\(\alpha < 1 \\) - hazard decrease with time
    - **Cox Proportional Hazards**
        - \\( b_0 \\) is a function of time 
        - the algo can estimate \\( b_1, b_2, .... \\) without having to specify the funtion for \\( b_0 \\)
        - good for analyzing hazard ratios: **how effective** is treatment A vs B, exposure or non-exposure
        - **can't do predictive models on survival**
        
 ### Lifelines: Survival analysis in python

 - [Talk from the author](https://www.youtube.com/watch?v=XQfxndJH4UA)
 - Docs: https://lifelines.readthedocs.io/en/latest/index.html
 



---- 
[Coursera: AI for Medical Prognosis](https://www.coursera.org/learn/ai-for-medical-prognosis/home/welcome)
 
- **prognosis** vs diagnosis: 
    - prognosis = predicting the likely or expected development of a disease
- examples in medical practice:
    - CHA2DS2-VASc score for atrial fibrillation
    - MELD score for end-stage liver desease: 
        - \\( ln \\) terms 
        - contain an **intercept** = if all other values is 0, expected risk score 
    - ASCVD (Atherosclerotic Cardiovascular Disease) Risk Calculator
        - **interaction terms** - capture dependence btw variables 
            - e.g. blood pressure has less effect of risk when patient is older 

## Evaluating risk scores
- Concordant Pairs: 
    - ![](/assets/images/2020-11-23-15-38-09.png)
    - Concordant = patient with worse outcome has higher risk score
    - if outcome ties => exclude
    - if outcome different => permissible pair => inlcude   
    - rule:
        - +1 for permissible pair that is Concordant
        - +0.5 for permissible pair with risk tie (outcome different, but same risk score)
- C-index 

    \\( C-index = { Count_{concordant} + 0.5 Count_{ties} \over Count_{permissible}} \\)
- Applying c-index on censored data - **Harrel's C-Index**
    - patient A & B both not censored => always permissible, even if A & B has same time-to-event
    - patient A & B both censored => not permissible
    - patient A censored, B not censored:
        - if A < B - not permissible
        - if A >= B - permissible
    ![](/assets/images/2020-11-23-16-40-58.png)
