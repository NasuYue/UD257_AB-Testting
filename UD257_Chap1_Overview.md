# Chapter 1: Overview of A/B Testing

> Introduction to A/B Testing | Udacity Free Courses
> https://www.udacity.com/course/ab-testing--ud257


- [Chapter 1: Overview of A/B Testing](#chapter-1-overview-of-ab-testing)
  - [Sec.1-7 Overview](#sec1-7-overview)
    - [Premise](#premise)
    - [What's A/B Testing](#whats-ab-testing)
  - [Sec.8-17 Business Example](#sec8-17-business-example)
    - [Binomial Distribution](#binomial-distribution)
    - [Sec.14 Caculating confidentail interval](#sec14-caculating-confidentail-interval)
    - [Sec.15 Example & Quiz](#sec15-example--quiz)
    - [Sec.16-17](#sec16-17)
  - [Sec.18-19 Comparing two samples: pooled standard error](#sec18-19-comparing-two-samples-pooled-standard-error)
    - [Sec.21-23 statistic power, power tradeoff size](#sec21-23-statistic-power-power-tradeoff-size)
    - [Sec.24 Calculating Number of Pages Views Needed](#sec24-calculating-number-of-pages-views-needed)
    - [Reference](#reference)

## Sec.1-7 Overview

### Premise
- AB testing is using statistics about Design and analyze experiment
- Process
    1. Choose a metric
    2. Review statistics
    3. Design
    4. Analyze

### What's A/B Testing
- use contronl (existing festure) and experiment (new feature) to find out which is better to user
- Expect robust and repeatable result > make decision of launching feature
- in online, your data with lower resolution, you cannot distinguish each user (vs clinical data)
- help you to climb the perk of current mountain,  not for  "choosing the right mountain" 
- AB testing doesn't apply to new experience
    - what's the baseline
    - how long does it take to accept the new experience
    - cannot tell you what's missing

Example
- Based on customer funnel model, to increase more student use "Adacity"
- Does new button help user enter the second level of funnel?
- hypothesis: change "start" button from orange to pink will increse ***how many students explore audacity courses***

Metrics:
1. Total number of course comleted > bad, too much time to verifiy
2. CTR=(number of click/number of page views) > hard, if a version of page with higher of clicks and the result is not accurate
3. CTP=(uniquue visitor who click/unique visitors ot page)> better, click-through-probability

>> updated hypothesis: Change "start" button from orange to pink will increse ***"click-through-probability"***

Note: rate vs probability 
1. Rate: the usability of a button, how often they find the button
2. Probability: trial clicks / page views, how many user enter 2nd level pages, filter out reload, wrong cliks...etc


## Sec.8-17 Business Example

### Binomial Distribution
- Pros: use formula to know how variable of overall CTP
- Assumption
    - Two types of outcomees
    - independant event : tricky part
    - identical distribution: p same for all


### Sec.14 Caculating confidentail interval
單樣本比例檢定

- p=p-hat=x/N
- SE=sqrt(p*(1-p)/total trail)
- Margin of error=z-score*SE
- CI=[p-SE,p+SE]
- rule of thumb: if N*p-hat>5 & N*(1-p-hat)>5 then use normnal distribution


### Sec.15 Example & Quiz

x=400
N=2000

p=300/2000=0.15
SE=sqrt(0.15*0.85/2000)

z-score 99%=2.58

M=2.58*sqrt(0.15*0.85/2000)=0.0205996481

CI=[p-SE,p+SE]=[0.1294,0.17063]

### Sec.16-17

單尾：是否有變化
雙尾：是否有增加or減少

H0:Pcont=Pexp
H1:Pcont=\=Pcont

Process
1. Mesure Pcont and Pexp
2. Caculate P(Pexp-Pcont|H0)
3. Reject null if alpha<0.05



## Sec.18-19 Comparing two samples: pooled standard error
雙樣本比例檢定 

Sample1:Xcont, Ncount
Sample2:Xexp, Nexp 
Ppool=(Xcount+Xexp)/(Ncout+Nexp)

**NOTE**
- what change matter to us? substantive = practically significance
- In medical or tranditional science, need 5-15% change to really be substantive. 
- In online biz like google, ***1-2%*** is quite large
- You want repeatability. It's statistical significant
- Sizing statistical significant bar is actually lower than practical significance bar

### Sec.21-23 statistic power, power tradeoff size
- to measure smaller change or higher result cofidence  > more sclae of experienment

- alpha = p(reject null |null true)
- beta = p(fail to reject|null false)
- power=sensibility = 1-beta (often 80%)
- confidence level = 1-alpha
- practical significance = minimum detectable effect = dmin (detect 最小改變量)

Example: how many page views affect sensibility

1. less sample size
    - alpha low, beta high
    - easy to fail to reject null
    - sensibility is low

2. more sample size
    - beta low
    - power increase
    - easy to reject null > sensitive

### Sec.24 Calculating Number of Pages Views Needed

***[Hypothesis]***
1. Initial
H0:Pcont=Pexp
H1:Pcont=\=Pcont

2. Updated
H0: Pexp-Pcont > dmin
H1: Pexp-Pcont =< dmin

***[Estimation]***
d-hat= Pexp-Pcont
dmin=minimum detectable effect, use 2% here.

confidential level = often use 95% 

SE=sqrt(p*(1-p)*((1/n1)+(1/n2)))
m=z-score*SE

CI=[d-m,d+m]

***[Decision]***
If dmin not in CI, then reject null. Otherwise, accept null.



---
### Reference

https://www.dataquest.io/blog/a-b-testing-the-definitive-guide-to-improving-your-product/

https://www.evanmiller.org/ab-testing/sample-size.html