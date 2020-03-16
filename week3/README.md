# The analysis of income in San Francisco 

## -For The San Francisco Chronicle Newspaper

## --Analyzed by Marco Lin 

## 2019/01/31


### The report is to analyze the cost of living in San Francisco for the San Francisco Chronicle newspaper. There are two main factors affect the cost of living: income and housing. As we know, the cost of living in San Francisco is high which is compared with other cities in the United States. As requested, We will analyze the data focusing on income in different aspects to show the different aspect of truth. It may help people to understand more about the structure of income, and give the advice to make a career decision. 


### The data we use is from Kaggle.com and the time is from 2013 to 2017. In our data, we have several elements of compensation. Salaries, other salaries, overtime pay, benefits, other benefits, health and Dental insurance, retirement.
### In addition, the data list the different jobs titles and classify the job into different departments and organizations that may help us to understand what the group of Jobs have more high salaries. 

### We also will make numerous ranks with the different part of salaries, such as overtime, insurance, and retirement for people who are looking for a job or who are planning a job career.

### Especially, in this report, we will explore the job which is better. We will compare with the total compensation and overtime to identify the benefits of the job. If the percentage of overtime take up a large part of total compensation, that means the job usually need to work over time. On the other hand, if the percentage of overtime take up a less part of total compensation and the compensation is on the top of the rank of compensation, it means this job is good to recommend. We will find the recommendations of jobs.

### In the final, we will explore the data to help our customer to understand the data and help to make business or policy decisions. 

## 1. Preparations

### - // Read the dataset and import the library "tidyverse" I need. 
### - // Checking the status of data, names of header, and summary the data 


```R
cops <- read.csv("~/Downloads/sf-employee-compensation/employee-compensation.csv")
library(tidyverse)
options(scipen=999)
str(cops)
names(cops)
summary(cops)
```

    ─ Attaching packages ──────────────────── tidyverse 1.2.1 ─
    ✔ ggplot2 3.0.0     ✔ purrr   0.2.5
    ✔ tibble  1.4.2     ✔ dplyr   0.7.6
    ✔ tidyr   0.8.1     ✔ stringr 1.3.1
    ✔ readr   1.1.1     ✔ forcats 0.3.0
    ─ Conflicts ───────────────────── tidyverse_conflicts() ─
    ✖ dplyr::filter() masks stats::filter()
    ✖ dplyr::lag()    masks stats::lag()


    'data.frame':	213202 obs. of  22 variables:
     $ Year.Type              : Factor w/ 1 level "Fiscal": 1 1 1 1 1 1 1 1 1 1 ...
     $ Year                   : int  2013 2014 2016 2015 2013 2015 2015 2015 2013 2015 ...
     $ Organization.Group.Code: int  1 2 2 2 2 2 2 1 3 6 ...
     $ Organization.Group     : Factor w/ 7 levels "Community Health",..: 6 7 7 7 7 7 7 6 5 3 ...
     $ Department.Code        : Factor w/ 56 levels "AAM","ADM","ADP",..: 29 38 4 38 22 38 38 19 23 46 ...
     $ Department             : Factor w/ 56 levels "AAM Asian Art Museum",..: 28 40 4 40 22 40 40 18 35 47 ...
     $ Union.Code             : int  798 261 790 253 21 21 790 790 535 790 ...
     $ Union                  : Factor w/ 78 levels "","Automotive Machinists, Local 1414",..: 20 27 64 76 57 57 64 64 63 64 ...
     $ Job.Family.Code        : Factor w/ 64 levels "","0900","1000",..: 56 43 7 49 31 31 12 44 21 7 ...
     $ Job.Family             : Factor w/ 58 levels "","Administrative & Mgmt (Unrep)",..: 19 51 10 55 41 41 48 27 23 10 ...
     $ Job.Code               : Factor w/ 1156 levels "0109","0111",..: 1113 860 155 1027 597 601 266 873 428 152 ...
     $ Job                    : Factor w/ 1162 levels "Account Clerk",..: 409 459 885 1100 559 410 719 1132 893 557 ...
     $ Employee.Identifier    : int  37216 24950 27447 42001 22142 56724 40114 50362 34064 49417 ...
     $ Salaries               : num  123841 61138 41193 66994 74261 ...
     $ Overtime               : num  76854 7341 0 26634 0 ...
     $ Other.Salaries         : num  14922 9219 390 4495 0 ...
     $ Total.Salary           : num  215617 77697 41583 98122 74261 ...
     $ Retirement             : num  24575 14898 6996 21232 13523 ...
     $ Health.Dental          : num  14920 12517 11309 13417 11989 ...
     $ Other.Benefits         : num  3590 6118 3201 7450 5977 ...
     $ Total.Benefits         : num  43085 33532 21506 42099 31490 ...
     $ Total.Compensation     : num  258702 111230 63089 140221 105750 ...



<ol class=list-inline>
	<li>'Year.Type'</li>
	<li>'Year'</li>
	<li>'Organization.Group.Code'</li>
	<li>'Organization.Group'</li>
	<li>'Department.Code'</li>
	<li>'Department'</li>
	<li>'Union.Code'</li>
	<li>'Union'</li>
	<li>'Job.Family.Code'</li>
	<li>'Job.Family'</li>
	<li>'Job.Code'</li>
	<li>'Job'</li>
	<li>'Employee.Identifier'</li>
	<li>'Salaries'</li>
	<li>'Overtime'</li>
	<li>'Other.Salaries'</li>
	<li>'Total.Salary'</li>
	<li>'Retirement'</li>
	<li>'Health.Dental'</li>
	<li>'Other.Benefits'</li>
	<li>'Total.Benefits'</li>
	<li>'Total.Compensation'</li>
</ol>




      Year.Type           Year      Organization.Group.Code
     Fiscal:213202   Min.   :2013   Min.   :1.000          
                     1st Qu.:2014   1st Qu.:2.000          
                     Median :2015   Median :2.000          
                     Mean   :2015   Mean   :2.982          
                     3rd Qu.:2016   3rd Qu.:4.000          
                     Max.   :2017   Max.   :7.000          
                                                           
                                    Organization.Group Department.Code
     Community Health                        :46121    DPH    :46121  
     Culture & Recreation                    :19738    MTA    :31059  
     General Administration & Finance        :19440    DSS    :17355  
     General City Responsibilities           :  266    POL    :16972  
     Human Welfare & Neighborhood Development:19594    REC    :12385  
     Public Protection                       :40754    AIR    : 9963  
     Public Works, Transportation & Commerce :67289    (Other):79347  
                             Department      Union.Code   
     DPH Public Health            :46121   Min.   :  1.0  
     MTA Municipal Transprtn Agncy:31059   1st Qu.:236.0  
     HSA Human Services Agency    :17355   Median :535.0  
     POL Police                   :16972   Mean   :491.3  
     REC Recreation & Park Commsn :12385   3rd Qu.:790.0  
     AIR Airport Commission       : 9963   Max.   :990.0  
     (Other)                      :79347   NA's   :215    
                                                    Union       Job.Family.Code 
     SEIU - Miscellaneous, Local 1021                  :60811   2300   : 21856  
     Prof & Tech Engineers - Miscellaneous, Local 21   :27369   9100   : 17372  
     SEIU - Staff and Per Diem Nurses, Local 1021      :16040   Q000   : 13905  
     Police Officers' Association                      :13901   7300   : 12440  
     Transport Workers - Transit Operators, Local 250-A:13089   9900   : 11088  
     SEIU - Health Workers, Local 1021                 :11804   2900   : 10838  
     (Other)                                           :70188   (Other):125703  
                   Job.Family        Job.Code     
     Nursing            : 21856   9163   : 13089  
     Street Transit     : 17372   P103   :  7663  
     Police Services    : 13905   2320   :  6621  
     Journeyman Trade   : 12440   H002   :  4249  
     Public Service Aide: 11088   9910   :  4221  
     Human Services     : 10838   9916   :  4171  
     (Other)            :125703   (Other):173188  
                               Job         Employee.Identifier    Salaries     
     Transit Operator            : 13089   Min.   :    1       Min.   :-68772  
     Special Nurse               :  7663   1st Qu.:14219       1st Qu.: 23166  
     Registered Nurse            :  6621   Median :28508       Median : 63211  
     Firefighter                 :  4249   Mean   :28504       Mean   : 63819  
     Public Service Trainee      :  4221   3rd Qu.:42839       3rd Qu.: 93215  
     Public Svc Aide-Public Works:  4171   Max.   :56987       Max.   :533986  
     (Other)                     :173188                                       
        Overtime      Other.Salaries      Total.Salary      Retirement    
     Min.   :-12309   Min.   :-19131.1   Min.   :-68772   Min.   :-28723  
     1st Qu.:     0   1st Qu.:     0.0   1st Qu.: 25101   1st Qu.:  3204  
     Median :     0   Median :   690.7   Median : 68642   Median : 12838  
     Mean   :  4510   Mean   :  3744.7   Mean   : 72074   Mean   : 12623  
     3rd Qu.:  2872   3rd Qu.:  4536.9   3rd Qu.:104365   3rd Qu.: 19117  
     Max.   :227314   Max.   :336726.3   Max.   :533986   Max.   :101306  
                                                                          
     Health.Dental   Other.Benefits  Total.Benefits   Total.Compensation
     Min.   :-2947   Min.   :-9858   Min.   :-19814   Min.   :-74083    
     1st Qu.: 4272   1st Qu.: 1578   1st Qu.:  9302   1st Qu.: 35380    
     Median :12133   Median : 4395   Median : 30311   Median : 98783    
     Mean   : 9054   Mean   : 4721   Mean   : 26399   Mean   : 98473    
     3rd Qu.:12829   3rd Qu.: 6950   3rd Qu.: 38498   3rd Qu.:143208    
     Max.   :22270   Max.   :36815   Max.   :138504   Max.   :668412    
                                                                        



```R
levels(cops$Organization.Group)
cops$Organization.Group.Code <- factor(cops$Organization.Group.Code)
```


<ol class=list-inline>
	<li>'Community Health'</li>
	<li>'Culture &amp; Recreation'</li>
	<li>'General Administration &amp; Finance'</li>
	<li>'General City Responsibilities'</li>
	<li>'Human Welfare &amp; Neighborhood Development'</li>
	<li>'Public Protection'</li>
	<li>'Public Works, Transportation &amp; Commerce'</li>
</ol>



# 2. Compensation percentage 

### - // We compare with two different time of period of compensation. First one is average of all data. Second one uses the data in 2017. The result shows that the component of compensation is the same from 2013~2017. It have not changed by the time.


```R
library(ggplot2)

ave_TC <- mean(cops$Total.Compensation)
ave_S <- mean(cops$Salaries)
ave_O <- mean(cops$Overtime)
ave_OS <- mean(cops$Other.Salaries)
ave_R <- mean(cops$Retirement)
ave_HD <- mean(cops$Health.Dental)
ave_OB <- mean(cops$Other.Benefits)

ave_pie <- data.frame(ave_TC = c("Salaries", "Overtime", "Other.Salaries", 
                                 "Retirement", "Health.Dental","Other.Benefits"),
                      perc=c(ave_S,ave_O,ave_OS,ave_R,ave_HD,ave_OB))
                 ave_pie = ave_pie[order(ave_pie$perc, decreasing = TRUE),]
                     myLabel = as.vector(ave_pie$ave_TC)  
                    myLabel = paste(myLabel, "(", round(ave_pie$perc / sum(ave_pie$perc) * 100, 2), " %) ", sep = "")  
                      
                 
ggplot((data=ave_pie),aes(x=factor(1), y=perc, fill=ave_TC)) +
    geom_bar(stat = "identity", width = 1 ) +
    coord_polar("y") +
    labs(x = "", y = "", title = "Percentage of Average Compensation") +
    theme(legend.title = element_blank(), legend.position = "top")+
    theme(axis.text.x = element_blank())  +
    scale_fill_discrete(breaks = ave_pie$ave_TC, labels = myLabel)+
    geom_text(x = 0, y = 0, label = "Salaries", alpha = 0.2)+
    geom_text(x = 0.3, y = 5, label = "Retirement                                                                      ", alpha = 0.2)+
    geom_text(x = 0.75, y = 40, label = "Overtime                                                                                         ", alpha = 0.2)+
    geom_text(x = 1, y = 50, label = "Other.Salaries                                                                                                     ", alpha = 0.2)+
    geom_text(x = 1.2, y =0, label = "other Benefits                                                                                       ", alpha = 0.2)+
    geom_text(x = 1.5, y = 20, label = "Health.Dental                                      ", alpha = 0.2)
 

cops2017 <- cops %>% filter(Year == "2017")
ave_TC_2017 <- mean(cops2017$Total.Compensation)
ave_S_2017 <- mean(cops2017$Salaries)
ave_O_2017 <- mean(cops2017$Overtime)
ave_OS_2017 <- mean(cops2017$Other.Salaries)
ave_R_2017 <- mean(cops2017$Retirement)
ave_HD_2017 <- mean(cops2017$Health.Dental)
ave_OB_2017 <- mean(cops2017$Other.Benefits)

ave_pie_2017 <- data.frame(ave_TC_2017 = c("Salaries_2017", "Overtime_2017", "Other.Salaries_2017", 
                                 "Retirement_2017", "Health.Denta_2017l","Other.Benefits_2017"),
                      perc_2017 =c(ave_S_2017,ave_O_2017,ave_OS_2017,ave_R_2017,ave_HD_2017,ave_OB_2017))
                 ave_pie_2017 = ave_pie_2017[order(ave_pie_2017$perc_2017, decreasing = TRUE),] 
                     myLabel = as.vector(ave_pie_2017$ave_TC_2017) 
                    myLabel = paste(myLabel, "(", round(ave_pie_2017$perc_2017 / sum(ave_pie_2017$perc_2017) * 100, 2), " %) ", sep = "")  
                      
                 
ggplot((data=ave_pie_2017),aes(x=factor(1), y=perc_2017, fill=ave_TC_2017)) +
    geom_bar(stat = "identity", width = 1 ) +
    coord_polar("y") +
    labs(x = "", y = "", title = "Percentage of Compensation in 2017") +
    theme(legend.title = element_blank(), legend.position = "top")+
    theme(axis.text.x = element_blank())  +
    scale_fill_discrete(breaks = ave_pie_2017$ave_TC_2017, labels = myLabel)+
    geom_text(x = 0, y = 0, label = "Salaries_2017", alpha = 0.2)+
    geom_text(x = 0.3, y = 5, label = "Retirement_2017                                                                     ", alpha = 0.2)+
    geom_text(x = 0.75, y = 40, label = "Overtime_2017                                                                                       ", alpha = 0.2)+
    geom_text(x = 1, y = 50, label = "Other.Salaries_2017                                                                                                   ", alpha = 0.2)+
    geom_text(x = 1.2, y =0, label = "other Benefits_2017                                                                                     ", alpha = 0.2)+
    geom_text(x = 1.5, y = 20, label = "Health.Dental_2017                                    ", alpha = 0.2)
```






![png](output_8_2.png)



![png](output_8_3.png)


# The tendency of Total Compensation


```R
cou2017 <- cops %>% filter(Year =="2017")
cou2016 <- cops %>% filter(Year =="2016")
cou2015 <- cops %>% filter(Year =="2015")
cou2014 <- cops %>% filter(Year =="2014")
cou2013 <- cops %>% filter(Year =="2013")

couData<-data_frame(Year=c("2017","2016","2015","2014","2013"),
                 Salaries=c(mean(cou2017$Total.Compensation),
                            mean(cou2016$Total.Compensation),
                            mean(cou2015$Total.Compensation),
                            mean(cou2014$Total.Compensation),
                            mean(cou2013$Total.Compensation)))

qplot(Year,Salaries, data = couData,
geom = c('boxplot', "point"))

```




![png](output_10_1.png)


### - This chart shows that our compensation from 2013 to 2017 is increasing

# 3. a. Compare the total compensation from 2013 to 2017

### - We rank the total compensation and salaries in each year. In each cell, top is ranked by total compensation, and the bottom is ranked by salaries.

## "2013" 1. Rank order by total compensation 2. Rank order by Salaries


```R
Tcops_2013 <- cops %>% filter(Year == "2013")
    Tcops_2013s <- select (Tcops_2013, Organization.Group,Job,Total.Compensation, Salaries)
        head(Tcops_2013s[order(Tcops_2013s$Total.Compensation, decreasing = T),], n=10)
        head(Tcops_2013s[order(Tcops_2013s$Salaries, decreasing = T),], n=10)
```


<table>
<thead><tr><th></th><th scope=col>Organization.Group</th><th scope=col>Job</th><th scope=col>Total.Compensation</th><th scope=col>Salaries</th></tr></thead>
<tbody>
	<tr><th scope=row>26100</th><td>Public Protection                      </td><td>Battlion Chief, Fire Suppressi         </td><td>425631.5                               </td><td>147998.7                               </td></tr>
	<tr><th scope=row>22455</th><td>Public Protection                      </td><td>Chief Of Police                        </td><td>397266.2                               </td><td>305942.0                               </td></tr>
	<tr><th scope=row>19361</th><td>Public Protection                      </td><td>Chief, Fire Department                 </td><td>396756.2                               </td><td>302068.0                               </td></tr>
	<tr><th scope=row>4871</th><td>Public Protection                      </td><td>Battlion Chief, Fire Suppressi         </td><td>389304.6                               </td><td>174681.3                               </td></tr>
	<tr><th scope=row>23250</th><td>Public Protection                      </td><td>Battlion Chief, Fire Suppressi         </td><td>385316.2                               </td><td>179760.5                               </td></tr>
	<tr><th scope=row>15831</th><td>Public Works, Transportation &amp; Commerce                           </td><td><span style=white-space:pre-wrap>Executive Contract Employee   </span></td><td>382392.9                                                              </td><td>286156.5                                                              </td></tr>
	<tr><th scope=row>36583</th><td>Public Works, Transportation &amp; Commerce                           </td><td><span style=white-space:pre-wrap>Dept Head V                   </span></td><td>382060.8                                                              </td><td>302114.2                                                              </td></tr>
	<tr><th scope=row>30078</th><td><span style=white-space:pre-wrap>General Administration &amp; Finance       </span></td><td><span style=white-space:pre-wrap>Dept Head V                   </span>             </td><td>381144.2                                                                           </td><td>279879.2                                                                           </td></tr>
	<tr><th scope=row>4799</th><td>Public Protection                      </td><td>Battlion Chief, Fire Suppressi         </td><td>381072.5                               </td><td>178067.4                               </td></tr>
	<tr><th scope=row>14351</th><td>Public Protection                      </td><td>Lieutenant, Fire Suppression           </td><td>376970.6                               </td><td>131177.3                               </td></tr>
</tbody>
</table>




<table>
<thead><tr><th></th><th scope=col>Organization.Group</th><th scope=col>Job</th><th scope=col>Total.Compensation</th><th scope=col>Salaries</th></tr></thead>
<tbody>
	<tr><th scope=row>22455</th><td>Public Protection                      </td><td>Chief Of Police                        </td><td>397266.2                               </td><td>305942.0                               </td></tr>
	<tr><th scope=row>36583</th><td>Public Works, Transportation &amp; Commerce                         </td><td><span style=white-space:pre-wrap>Dept Head V                 </span></td><td>382060.8                                                            </td><td>302114.2                                                            </td></tr>
	<tr><th scope=row>19361</th><td>Public Protection                      </td><td>Chief, Fire Department                 </td><td>396756.2                               </td><td>302068.0                               </td></tr>
	<tr><th scope=row>20966</th><td>Public Works, Transportation &amp; Commerce                         </td><td><span style=white-space:pre-wrap>Gen Mgr, Public Trnsp Dept  </span></td><td>369054.7                                                            </td><td>294000.2                                                            </td></tr>
	<tr><th scope=row>15831</th><td>Public Works, Transportation &amp; Commerce</td><td>Executive Contract Employee                </td><td>382392.9                                   </td><td>286156.5                                   </td></tr>
	<tr><th scope=row>30078</th><td><span style=white-space:pre-wrap>General Administration &amp; Finance       </span></td><td><span style=white-space:pre-wrap>Dept Head V                 </span>               </td><td>381144.2                                                                           </td><td>279879.2                                                                           </td></tr>
	<tr><th scope=row>5366</th><td><span style=white-space:pre-wrap>General Administration &amp; Finance       </span></td><td>Dep Dir For Investments, Ret                                                       </td><td>347307.2                                                                           </td><td>273446.0                                                                           </td></tr>
	<tr><th scope=row>5792</th><td><span style=white-space:pre-wrap>General Administration &amp; Finance       </span></td><td><span style=white-space:pre-wrap>Mayor                       </span>               </td><td>346334.6                                                                           </td><td>272103.0                                                                           </td></tr>
	<tr><th scope=row>2527</th><td>Community Health                       </td><td>Adm, SFGH Medical Center               </td><td>342746.8                               </td><td>270058.0                               </td></tr>
	<tr><th scope=row>22393</th><td>Public Protection                      </td><td>Deputy Chief 3                         </td><td>342242.2                               </td><td>268632.0                               </td></tr>
</tbody>
</table>



## "2014" 1. Rank order by total compensation 2. Rank order by Salaries


```R
Tcops_2014 <- cops %>% filter(Year == "2014")
    Tcops_2014s <- select (Tcops_2014, Organization.Group,Job,Total.Compensation, Salaries)
        head(Tcops_2014s[order(Tcops_2014s$Total.Compensation, decreasing = T),] ,n=10)
                head(Tcops_2014s[order(Tcops_2014s$Salaries, decreasing = T),], n=10)
```


<table>
<thead><tr><th></th><th scope=col>Organization.Group</th><th scope=col>Job</th><th scope=col>Total.Compensation</th><th scope=col>Salaries</th></tr></thead>
<tbody>
	<tr><th scope=row>29708</th><td><span style=white-space:pre-wrap>General Administration &amp; Finance       </span></td><td><span style=white-space:pre-wrap>Asst Med Examiner             </span>             </td><td>433100.1                                                                           </td><td>267141.0                                                                           </td></tr>
	<tr><th scope=row>19354</th><td>Public Protection                      </td><td>Deputy Chief 3                         </td><td>425320.2                               </td><td>191142.0                               </td></tr>
	<tr><th scope=row>34221</th><td>Public Protection                      </td><td>Chief, Fire Department                 </td><td>416870.0                               </td><td>303229.8                               </td></tr>
	<tr><th scope=row>7932</th><td>Public Protection                      </td><td>Chief Of Police                        </td><td>413233.7                               </td><td>308632.5                               </td></tr>
	<tr><th scope=row>6693</th><td>Public Works, Transportation &amp; Commerce                           </td><td><span style=white-space:pre-wrap>Executive Contract Employee   </span></td><td>403817.5                                                              </td><td>306710.7                                                              </td></tr>
	<tr><th scope=row>27450</th><td>Public Works, Transportation &amp; Commerce                           </td><td><span style=white-space:pre-wrap>Dept Head V                   </span></td><td>402431.1                                                              </td><td>307760.6                                                              </td></tr>
	<tr><th scope=row>14137</th><td>Public Protection                      </td><td>Battlion Chief, Fire Suppressi         </td><td>392246.9                               </td><td>179464.1                               </td></tr>
	<tr><th scope=row>10727</th><td>Public Protection                      </td><td>Deputy Chief 3                         </td><td>390027.5                               </td><td>160146.0                               </td></tr>
	<tr><th scope=row>28205</th><td>Public Protection                      </td><td>Asst Chf Of Dept (Fire Dept)           </td><td>389757.4                               </td><td>205480.8                               </td></tr>
	<tr><th scope=row>24652</th><td>Community Health                       </td><td>Senior Physician Specialist            </td><td>387258.3                               </td><td>199638.9                               </td></tr>
</tbody>
</table>




<table>
<thead><tr><th></th><th scope=col>Organization.Group</th><th scope=col>Job</th><th scope=col>Total.Compensation</th><th scope=col>Salaries</th></tr></thead>
<tbody>
	<tr><th scope=row>7932</th><td>Public Protection                       </td><td>Chief Of Police                         </td><td>413233.7                                </td><td>308632.5                                </td></tr>
	<tr><th scope=row>27450</th><td>Public Works, Transportation &amp; Commerce                        </td><td><span style=white-space:pre-wrap>Dept Head V                </span></td><td>402431.1                                                           </td><td>307760.6                                                           </td></tr>
	<tr><th scope=row>6693</th><td>Public Works, Transportation &amp; Commerce </td><td>Executive Contract Employee                 </td><td>403817.5                                    </td><td>306710.7                                    </td></tr>
	<tr><th scope=row>34221</th><td>Public Protection                       </td><td>Chief, Fire Department                  </td><td>416870.0                                </td><td>303229.8                                </td></tr>
	<tr><th scope=row>5891</th><td>Public Works, Transportation &amp; Commerce </td><td>Gen Mgr, Public Trnsp Dept                  </td><td>386174.8                                    </td><td>295131.0                                    </td></tr>
	<tr><th scope=row>10665</th><td><span style=white-space:pre-wrap>General Administration &amp; Finance        </span></td><td><span style=white-space:pre-wrap>Mayor                      </span>                 </td><td>367052.3                                                                            </td><td>279158.5                                                                            </td></tr>
	<tr><th scope=row>36930</th><td>Community Health                        </td><td>Adm, SFGH Medical Center                </td><td>356942.9                                </td><td>271007.3                                </td></tr>
	<tr><th scope=row>12094</th><td>Community Health                        </td><td>Dept Head V                             </td><td>356391.8                                </td><td>267936.7                                </td></tr>
	<tr><th scope=row>29587</th><td>Human Welfare &amp; Neighborhood Development                       </td><td><span style=white-space:pre-wrap>Dept Head V                </span></td><td>356015.9                                                           </td><td>267936.6                                                           </td></tr>
	<tr><th scope=row>6211</th><td><span style=white-space:pre-wrap>General Administration &amp; Finance        </span></td><td><span style=white-space:pre-wrap>Dept Head V                </span>                 </td><td>353671.7                                                                            </td><td>267936.6                                                                            </td></tr>
</tbody>
</table>



## "2015" 1. Rank order by total compensation 2. Rank order by Salaries


```R
Tcops_2015 <- cops %>% filter(Year == "2015")
    Tcops_2015s <- select (Tcops_2015, Organization.Group,Job,Total.Compensation, Salaries)
        head(Tcops_2015s[order(Tcops_2015s$Total.Compensation, decreasing = T),] ,n=10)
        head(Tcops_2015s[order(Tcops_2015s$Salaries, decreasing = T),], n=10)
```


<table>
<thead><tr><th></th><th scope=col>Organization.Group</th><th scope=col>Job</th><th scope=col>Total.Compensation</th><th scope=col>Salaries</th></tr></thead>
<tbody>
	<tr><th scope=row>12573</th><td><span style=white-space:pre-wrap>General Administration &amp; Finance       </span></td><td><span style=white-space:pre-wrap>Asst Med Examiner          </span>                </td><td>497505.9                                                                           </td><td>276342.3                                                                           </td></tr>
	<tr><th scope=row>3312</th><td><span style=white-space:pre-wrap>General Administration &amp; Finance       </span></td><td><span style=white-space:pre-wrap>Chief Investment Officer   </span>                </td><td>495721.5                                                                           </td><td>379201.7                                                                           </td></tr>
	<tr><th scope=row>40089</th><td><span style=white-space:pre-wrap>General Administration &amp; Finance       </span></td><td><span style=white-space:pre-wrap>Asst Med Examiner          </span>                </td><td>460272.2                                                                           </td><td>276342.3                                                                           </td></tr>
	<tr><th scope=row>28311</th><td>Public Protection                      </td><td>Deputy Chief 3                         </td><td>438159.4                               </td><td>221104.8                               </td></tr>
	<tr><th scope=row>5551</th><td>Public Protection                      </td><td>Chief, Fire Department                 </td><td>424563.3                               </td><td>303229.8                               </td></tr>
	<tr><th scope=row>12781</th><td>Public Works, Transportation &amp; Commerce                        </td><td><span style=white-space:pre-wrap>Dept Head V                </span></td><td>422449.0                                                           </td><td>318344.8                                                           </td></tr>
	<tr><th scope=row>30602</th><td>Public Protection                      </td><td>Chief Of Police                        </td><td>420516.1                               </td><td>308632.6                               </td></tr>
	<tr><th scope=row>31306</th><td>Public Works, Transportation &amp; Commerce</td><td>Executive Contract Employee                </td><td>419936.2                                   </td><td>317112.8                                   </td></tr>
	<tr><th scope=row>10897</th><td>Public Works, Transportation &amp; Commerce</td><td>Executive Contract Employee                </td><td>409466.3                                   </td><td>198862.0                                   </td></tr>
	<tr><th scope=row>21276</th><td><span style=white-space:pre-wrap>General Administration &amp; Finance       </span></td><td><span style=white-space:pre-wrap>Asst Med Examiner          </span>                </td><td>407999.8                                                                           </td><td>238677.5                                                                           </td></tr>
</tbody>
</table>




<table>
<thead><tr><th></th><th scope=col>Organization.Group</th><th scope=col>Job</th><th scope=col>Total.Compensation</th><th scope=col>Salaries</th></tr></thead>
<tbody>
	<tr><th scope=row>3312</th><td><span style=white-space:pre-wrap>General Administration &amp; Finance       </span></td><td><span style=white-space:pre-wrap>Chief Investment Officer                </span>   </td><td>495721.5                                                                           </td><td>379201.7                                                                           </td></tr>
	<tr><th scope=row>12781</th><td>Public Works, Transportation &amp; Commerce                                     </td><td><span style=white-space:pre-wrap>Dept Head V                             </span></td><td>422449.0                                                                        </td><td>318344.8                                                                        </td></tr>
	<tr><th scope=row>31306</th><td>Public Works, Transportation &amp; Commerce                                     </td><td><span style=white-space:pre-wrap>Executive Contract Employee             </span></td><td>419936.2                                                                        </td><td>317112.8                                                                        </td></tr>
	<tr><th scope=row>30602</th><td>Public Protection                       </td><td>Chief Of Police                         </td><td>420516.1                                </td><td>308632.6                                </td></tr>
	<tr><th scope=row>5551</th><td>Public Protection                       </td><td>Chief, Fire Department                  </td><td>424563.3                                </td><td>303229.8                                </td></tr>
	<tr><th scope=row>23843</th><td>Community Health                        </td><td>Dept Head V                             </td><td>401962.9                                </td><td>302512.9                                </td></tr>
	<tr><th scope=row>37622</th><td>Public Works, Transportation &amp; Commerce                                     </td><td><span style=white-space:pre-wrap>Gen Mgr, Public Trnsp Dept              </span></td><td>401619.5                                                                        </td><td>299066.0                                                                        </td></tr>
	<tr><th scope=row>2032</th><td>Community Health                        </td><td>Administrator, Department Of Public Heal</td><td>385268.0                                </td><td>289017.1                                </td></tr>
	<tr><th scope=row>8038</th><td><span style=white-space:pre-wrap>General Administration &amp; Finance       </span></td><td><span style=white-space:pre-wrap>Mayor                                   </span>   </td><td>382096.3                                                                           </td><td>286416.4                                                                           </td></tr>
	<tr><th scope=row>12573</th><td><span style=white-space:pre-wrap>General Administration &amp; Finance       </span></td><td><span style=white-space:pre-wrap>Asst Med Examiner                       </span>   </td><td>497505.9                                                                           </td><td>276342.3                                                                           </td></tr>
</tbody>
</table>



## "2016" 1. Rank order by total compensation 2. Rank order by Salaries


```R
Tcops_2016 <- cops %>% filter(Year == "2016")
    Tcops_2016s <- select (Tcops_2016, Organization.Group,Job,Total.Compensation, Salaries)
        head(Tcops_2016s[order(Tcops_2016s$Total.Compensation, decreasing = T),] ,n=10)
        head(Tcops_2016s[order(Tcops_2016s$Salaries, decreasing = T),], n=10)
```


<table>
<thead><tr><th></th><th scope=col>Organization.Group</th><th scope=col>Job</th><th scope=col>Total.Compensation</th><th scope=col>Salaries</th></tr></thead>
<tbody>
	<tr><th scope=row>6979</th><td><span style=white-space:pre-wrap>General Administration &amp; Finance       </span></td><td><span style=white-space:pre-wrap>Chief Investment Officer   </span>                </td><td>653605.3                                                                           </td><td>515101.8                                                                           </td></tr>
	<tr><th scope=row>35096</th><td>Public Protection                      </td><td>Chief Of Police                        </td><td>466893.1                               </td><td>292450.1                               </td></tr>
	<tr><th scope=row>38034</th><td><span style=white-space:pre-wrap>General Administration &amp; Finance       </span></td><td><span style=white-space:pre-wrap>Dept Head V                </span>                </td><td>433409.9                                                                           </td><td>329237.3                                                                           </td></tr>
	<tr><th scope=row>15032</th><td>Public Works, Transportation &amp; Commerce                        </td><td><span style=white-space:pre-wrap>Dept Head V                </span></td><td>430979.8                                                           </td><td>334779.1                                                           </td></tr>
	<tr><th scope=row>34738</th><td>Public Protection                      </td><td>Chief, Fire Department                 </td><td>426114.0                               </td><td>307430.8                               </td></tr>
	<tr><th scope=row>3032</th><td>Public Works, Transportation &amp; Commerce</td><td>Executive Contract Employee                </td><td>422127.0                                   </td><td>328434.4                                   </td></tr>
	<tr><th scope=row>6173</th><td>Community Health                       </td><td>Senior Physician Specialist            </td><td>418120.8                               </td><td>233936.4                               </td></tr>
	<tr><th scope=row>26296</th><td>Public Works, Transportation &amp; Commerce</td><td>Gen Mgr, Public Trnsp Dept                 </td><td>410566.7                                   </td><td>312303.7                                   </td></tr>
	<tr><th scope=row>25348</th><td>Community Health                       </td><td>Dept Head V                            </td><td>408264.6                               </td><td>316368.5                               </td></tr>
	<tr><th scope=row>3464</th><td>Public Protection                      </td><td>Deputy Sheriff                         </td><td>402311.7                               </td><td>100724.1                               </td></tr>
</tbody>
</table>




<table>
<thead><tr><th></th><th scope=col>Organization.Group</th><th scope=col>Job</th><th scope=col>Total.Compensation</th><th scope=col>Salaries</th></tr></thead>
<tbody>
	<tr><th scope=row>6979</th><td><span style=white-space:pre-wrap>General Administration &amp; Finance       </span></td><td><span style=white-space:pre-wrap>Chief Investment Officer                </span>   </td><td>653605.3                                                                           </td><td>515101.8                                                                           </td></tr>
	<tr><th scope=row>15032</th><td>Public Works, Transportation &amp; Commerce                                     </td><td><span style=white-space:pre-wrap>Dept Head V                             </span></td><td>430979.8                                                                        </td><td>334779.1                                                                        </td></tr>
	<tr><th scope=row>38034</th><td><span style=white-space:pre-wrap>General Administration &amp; Finance       </span></td><td><span style=white-space:pre-wrap>Dept Head V                             </span>   </td><td>433409.9                                                                           </td><td>329237.3                                                                           </td></tr>
	<tr><th scope=row>3032</th><td>Public Works, Transportation &amp; Commerce                                     </td><td><span style=white-space:pre-wrap>Executive Contract Employee             </span></td><td>422127.0                                                                        </td><td>328434.4                                                                        </td></tr>
	<tr><th scope=row>25348</th><td>Community Health                        </td><td>Dept Head V                             </td><td>408264.6                                </td><td>316368.5                                </td></tr>
	<tr><th scope=row>26296</th><td>Public Works, Transportation &amp; Commerce                                     </td><td><span style=white-space:pre-wrap>Gen Mgr, Public Trnsp Dept              </span></td><td>410566.7                                                                        </td><td>312303.7                                                                        </td></tr>
	<tr><th scope=row>34738</th><td>Public Protection                       </td><td>Chief, Fire Department                  </td><td>426114.0                                </td><td>307430.8                                </td></tr>
	<tr><th scope=row>39638</th><td>Community Health                        </td><td>Administrator, Department Of Public Heal</td><td>395733.6                                </td><td>306398.6                                </td></tr>
	<tr><th scope=row>40077</th><td><span style=white-space:pre-wrap>General Administration &amp; Finance       </span></td><td><span style=white-space:pre-wrap>Mayor                                   </span>   </td><td>382731.8                                                                           </td><td>295276.9                                                                           </td></tr>
	<tr><th scope=row>35096</th><td>Public Protection                       </td><td>Chief Of Police                         </td><td>466893.1                                </td><td>292450.1                                </td></tr>
</tbody>
</table>



## "2017" 1. Rank order by total compensation 2. Rank order by Salaries


```R
Tcops_2017 <- cops %>% filter(Year == "2017")
    Tcops_2017s <- select (Tcops_2017, Organization.Group,Job,Total.Compensation, Salaries)
        head(Tcops_2017s[order(Tcops_2017s$Total.Compensation, decreasing = T),] ,n=10)
        head(Tcops_2017s[order(Tcops_2017s$Salaries, decreasing = T),], n=10)
```


<table>
<thead><tr><th></th><th scope=col>Organization.Group</th><th scope=col>Job</th><th scope=col>Total.Compensation</th><th scope=col>Salaries</th></tr></thead>
<tbody>
	<tr><th scope=row>16694</th><td><span style=white-space:pre-wrap>General Administration &amp; Finance       </span></td><td><span style=white-space:pre-wrap>Chief Investment Officer    </span>               </td><td>668412.4                                                                           </td><td>533985.9                                                                           </td></tr>
	<tr><th scope=row>40344</th><td>Community Health                       </td><td>Physician Administrator, DPH           </td><td>538791.7                               </td><td>418016.6                               </td></tr>
	<tr><th scope=row>33877</th><td><span style=white-space:pre-wrap>General Administration &amp; Finance       </span></td><td><span style=white-space:pre-wrap>Managing Director           </span>               </td><td>532690.6                                                                           </td><td>420076.6                                                                           </td></tr>
	<tr><th scope=row>9459</th><td>Public Works, Transportation &amp; Commerce                         </td><td><span style=white-space:pre-wrap>Transit Operator            </span></td><td>479167.2                                                            </td><td>355340.6                                                            </td></tr>
	<tr><th scope=row>10158</th><td><span style=white-space:pre-wrap>General Administration &amp; Finance       </span></td><td><span style=white-space:pre-wrap>Dept Head V                 </span>               </td><td>452385.2                                                                           </td><td>346944.0                                                                           </td></tr>
	<tr><th scope=row>39784</th><td>Public Protection                      </td><td>Chief, Fire Department                 </td><td>443297.1                               </td><td>312390.9                               </td></tr>
	<tr><th scope=row>36917</th><td>Community Health                       </td><td>Senior Physician Specialist            </td><td>436540.5                               </td><td>243095.4                               </td></tr>
	<tr><th scope=row>29056</th><td>Public Works, Transportation &amp; Commerce</td><td>Executive Contract Employee                </td><td>436449.8                                   </td><td>340344.0                                   </td></tr>
	<tr><th scope=row>26522</th><td><span style=white-space:pre-wrap>General Administration &amp; Finance       </span></td><td><span style=white-space:pre-wrap>Managing Director           </span>               </td><td>427395.4                                                                           </td><td>320644.3                                                                           </td></tr>
	<tr><th scope=row>38258</th><td>Public Protection                      </td><td>Sheriff's Lieutenant                   </td><td>427324.1                               </td><td>138857.5                               </td></tr>
</tbody>
</table>




<table>
<thead><tr><th></th><th scope=col>Organization.Group</th><th scope=col>Job</th><th scope=col>Total.Compensation</th><th scope=col>Salaries</th></tr></thead>
<tbody>
	<tr><th scope=row>16694</th><td><span style=white-space:pre-wrap>General Administration &amp; Finance       </span></td><td><span style=white-space:pre-wrap>Chief Investment Officer                </span>   </td><td>668412.4                                                                           </td><td>533985.9                                                                           </td></tr>
	<tr><th scope=row>33877</th><td><span style=white-space:pre-wrap>General Administration &amp; Finance       </span></td><td><span style=white-space:pre-wrap>Managing Director                       </span>   </td><td>532690.6                                                                           </td><td>420076.6                                                                           </td></tr>
	<tr><th scope=row>40344</th><td>Community Health                        </td><td>Physician Administrator, DPH            </td><td>538791.7                                </td><td>418016.6                                </td></tr>
	<tr><th scope=row>9459</th><td>Public Works, Transportation &amp; Commerce                                     </td><td><span style=white-space:pre-wrap>Transit Operator                        </span></td><td>479167.2                                                                        </td><td>355340.6                                                                        </td></tr>
	<tr><th scope=row>10158</th><td><span style=white-space:pre-wrap>General Administration &amp; Finance       </span></td><td><span style=white-space:pre-wrap>Dept Head V                             </span>   </td><td>452385.2                                                                           </td><td>346944.0                                                                           </td></tr>
	<tr><th scope=row>29056</th><td>Public Works, Transportation &amp; Commerce                                     </td><td><span style=white-space:pre-wrap>Executive Contract Employee             </span></td><td>436449.8                                                                        </td><td>340344.0                                                                        </td></tr>
	<tr><th scope=row>5744</th><td>Community Health                        </td><td>Dept Head V                             </td><td>424592.3                                </td><td>329470.3                                </td></tr>
	<tr><th scope=row>35149</th><td>Public Works, Transportation &amp; Commerce                                     </td><td><span style=white-space:pre-wrap>Gen Mgr, Public Trnsp Dept              </span></td><td>425119.9                                                                        </td><td>324064.9                                                                        </td></tr>
	<tr><th scope=row>26522</th><td><span style=white-space:pre-wrap>General Administration &amp; Finance       </span></td><td><span style=white-space:pre-wrap>Managing Director                       </span>   </td><td>427395.4                                                                           </td><td>320644.3                                                                           </td></tr>
	<tr><th scope=row>15127</th><td>Community Health                        </td><td>Administrator, Department Of Public Heal</td><td>408262.4                                </td><td>316781.3                                </td></tr>
</tbody>
</table>



### ---- In this object, the jobs of Public Protection were the highest salaries in 2013. Then, after 2014, the jobs of General Administration & Finance has started to replace the jobs of Public Protection, becoming the highest job in general. In 2017, the salaries of jobs of Public Protection is decreasing. So, in this result, we know the good job in 2017 is in General Administration & Finance field.

# *Vector


```R
JobTitle <- c("Chief Investment Officer","Physician Administrator, DPH", "Managing Director","Transit Operator","Dept Head V" )
JobTitle
```


<ol class=list-inline>
	<li>'Chief Investment Officer'</li>
	<li>'Physician Administrator, DPH'</li>
	<li>'Managing Director'</li>
	<li>'Transit Operator'</li>
	<li>'Dept Head V'</li>
</ol>



### -This vector I set is for the top five of high salaries in 2017. It is easy for people understand the what the popular job now.

# !Compare "the Chief Of Police" and "the Chief Investment Officer"!


```R
counts2017 <- cops %>% filter(Organization.Group == "Public Protection", Year =="2017", 
                              Job =="Chief Of Police", Employee.Identifier == "55717")
counts2016 <- cops %>% filter(Organization.Group == "Public Protection", Year =="2016", 
                              Job =="Chief Of Police", Employee.Identifier == "55717")
counts2015 <- cops %>% filter(Organization.Group == "Public Protection", Year =="2015", 
                              Job =="Chief Of Police",Employee.Identifier == "55717")
counts2014 <- cops %>% filter(Organization.Group == "Public Protection", Year =="2014", 
                              Job =="Chief Of Police",Employee.Identifier == "55717")
counts2013 <- cops %>% filter(Organization.Group == "Public Protection", Year =="2013", 
                              Job =="Chief Of Police",Employee.Identifier == "55717")
listSample<-data_frame(Year=c("2017","2016","2015","2014","2013"),
                 Salaries=c(mean(counts2017$Total.Compensation),
                            mean(counts2016$Total.Compensation),
                            mean(counts2015$Total.Compensation),
                            mean(counts2014$Total.Compensation),
                            mean(counts2017$Total.Compensation)))

p1 <- ggplot(listSample, aes(x = Year , y = Salaries)) + geom_bar(stat = "identity") + ggtitle("Chief Of Police") 
```


```R
Gcounts2017 <- cops %>% filter(Organization.Group == "General Administration & Finance", Year =="2017", Job =="Chief Investment Officer", Employee.Identifier =="33145")
Gcounts2016 <- cops %>% filter(Organization.Group == "General Administration & Finance", Year =="2016", Job =="Chief Investment Officer", Employee.Identifier =="33145")
Gcounts2015 <- cops %>% filter(Organization.Group == "General Administration & Finance", Year =="2015", Job =="Chief Investment Officer", Employee.Identifier =="33145")
Gcounts2014 <- cops %>% filter(Organization.Group == "General Administration & Finance", Year =="2014", Job =="Chief Investment Officer", Employee.Identifier =="33145")
Gcounts2013 <- cops %>% filter(Organization.Group == "General Administration & Finance", Year =="2013", Job =="Chief Investment Officer", Employee.Identifier =="33145")

GlistSample<-data_frame(Year=c("2017","2016","2015","2014","2013"),
                 Salaries=c(mean(Gcounts2017$Total.Compensation),
                            mean(Gcounts2016$Total.Compensation),
                            mean(Gcounts2015$Total.Compensation),
                            mean(Gcounts2014$Total.Compensation),
                            mean(Gcounts2013$Total.Compensation)))

p2 <- ggplot(GlistSample, aes( x = Year, y = Salaries)) + geom_bar(stat = "identity") + ggtitle("Chief Investment Officer") 


cowplot::plot_grid(p1,p2, ncol = 1, 
align = 'h', axis = 'l')

```

    Warning message:
    “Removed 1 rows containing missing values (position_stack).”




![png](output_30_2.png)


### - in this bar chart, we can see from 2014, the compensation of Chief investment Officer has been increasing. On the other hand, the compensation of the Chief of Police had increased from 2014 to 2016, but it have decreased in 2017. That why Chief investment Officer are on the top one of salaries now.

# 4. Jobs Advantage Difference

## a. Retirement Rank

### -// Use select function to pick up Organization.Group,Job, and Total.Compensation with different condition. and show the top 10.


```R
Tcops_2017R <- select (Tcops_2017, Organization.Group,Job, Retirement ,Total.Compensation)
        head(Tcops_2017R[order(Tcops_2017R$Retirement, decreasing = T),], n=10)
```


<table>
<thead><tr><th></th><th scope=col>Organization.Group</th><th scope=col>Job</th><th scope=col>Retirement</th><th scope=col>Total.Compensation</th></tr></thead>
<tbody>
	<tr><th scope=row>16694</th><td><span style=white-space:pre-wrap>General Administration &amp; Finance       </span></td><td><span style=white-space:pre-wrap>Chief Investment Officer    </span>               </td><td>95600.00                                                                           </td><td>668412.4                                                                           </td></tr>
	<tr><th scope=row>9459</th><td>Public Works, Transportation &amp; Commerce                         </td><td><span style=white-space:pre-wrap>Transit Operator            </span></td><td>93356.58                                                            </td><td>479167.2                                                            </td></tr>
	<tr><th scope=row>33877</th><td><span style=white-space:pre-wrap>General Administration &amp; Finance       </span></td><td><span style=white-space:pre-wrap>Managing Director           </span>               </td><td>75146.60                                                                           </td><td>532690.6                                                                           </td></tr>
	<tr><th scope=row>40344</th><td>Community Health                       </td><td>Physician Administrator, DPH           </td><td>74197.99                               </td><td>538791.7                               </td></tr>
	<tr><th scope=row>10158</th><td><span style=white-space:pre-wrap>General Administration &amp; Finance       </span></td><td><span style=white-space:pre-wrap>Dept Head V                 </span>               </td><td>61582.56                                                                           </td><td>452385.2                                                                           </td></tr>
	<tr><th scope=row>29056</th><td>Public Works, Transportation &amp; Commerce</td><td>Executive Contract Employee                </td><td>60411.06                                   </td><td>436449.8                                   </td></tr>
	<tr><th scope=row>39784</th><td>Public Protection                      </td><td>Chief, Fire Department                 </td><td>59310.43                               </td><td>443297.1                               </td></tr>
	<tr><th scope=row>5744</th><td>Community Health                       </td><td>Dept Head V                            </td><td>58480.96                               </td><td>424592.3                               </td></tr>
	<tr><th scope=row>35149</th><td>Public Works, Transportation &amp; Commerce                         </td><td><span style=white-space:pre-wrap>Gen Mgr, Public Trnsp Dept  </span></td><td>57521.53                                                            </td><td>425119.9                                                            </td></tr>
	<tr><th scope=row>26522</th><td><span style=white-space:pre-wrap>General Administration &amp; Finance       </span></td><td><span style=white-space:pre-wrap>Managing Director           </span>               </td><td>57119.52                                                                           </td><td>427395.4                                                                           </td></tr>
</tbody>
</table>



# b. Health/Dental Rank


```R
Tcops_2017H <- select (Tcops_2017,Organization.Group, Job, Health.Dental ,Total.Compensation)
        head(Tcops_2017H[order(Tcops_2017H$Health.Dental, decreasing = T),] , n=10)
```


<table>
<thead><tr><th></th><th scope=col>Organization.Group</th><th scope=col>Job</th><th scope=col>Health.Dental</th><th scope=col>Total.Compensation</th></tr></thead>
<tbody>
	<tr><th scope=row>18472</th><td>Public Protection        </td><td>Duty Officer             </td><td>22270.12                 </td><td>165057.7                 </td></tr>
	<tr><th scope=row>23851</th><td>Public Protection        </td><td>EMT/Paramedic/Firefighter</td><td>19304.20                 </td><td>247032.4                 </td></tr>
	<tr><th scope=row>40888</th><td>Public Protection        </td><td>Senior Deputy Sheriff    </td><td>18658.44                 </td><td>266037.3                 </td></tr>
	<tr><th scope=row>26742</th><td>Public Protection        </td><td>Firefighter              </td><td>18153.37                 </td><td>195839.9                 </td></tr>
	<tr><th scope=row>289</th><td>Public Protection        </td><td>Firefighter              </td><td>16930.04                 </td><td>190150.3                 </td></tr>
	<tr><th scope=row>534</th><td>Public Protection        </td><td>Firefighter              </td><td>16930.04                 </td><td>178417.4                 </td></tr>
	<tr><th scope=row>2232</th><td>Public Protection        </td><td>Firefighter              </td><td>16930.04                 </td><td>225436.3                 </td></tr>
	<tr><th scope=row>2256</th><td>Public Protection        </td><td>Firefighter              </td><td>16930.04                 </td><td>130454.0                 </td></tr>
	<tr><th scope=row>3182</th><td>Public Protection        </td><td>Firefighter              </td><td>16930.04                 </td><td>235636.4                 </td></tr>
	<tr><th scope=row>3510</th><td>Public Protection        </td><td>EMT/Paramedic/Firefighter</td><td>16930.04                 </td><td>215996.7                 </td></tr>
</tbody>
</table>



### - Public Protection Job get a lot of pay from Health and Dental. in addition, by connecting with the data below, the Public Protection Job is not a good choice for the person who just want to have a easy job.

# c. Overtime Rank


```R
Tcops_2017O <- select (Tcops_2017, Organization.Group,Job, Overtime ,Total.Compensation)
        head(Tcops_2017O[order(Tcops_2017O$Overtime, decreasing = T),] , n=10)
```


<table>
<thead><tr><th></th><th scope=col>Organization.Group</th><th scope=col>Job</th><th scope=col>Overtime</th><th scope=col>Total.Compensation</th></tr></thead>
<tbody>
	<tr><th scope=row>42289</th><td>Public Protection    </td><td>Deputy Sheriff       </td><td>203449.6             </td><td>393669.9             </td></tr>
	<tr><th scope=row>37897</th><td>Public Protection    </td><td>Deputy Sheriff       </td><td>200886.2             </td><td>386896.9             </td></tr>
	<tr><th scope=row>32522</th><td>Public Protection    </td><td>Deputy Sheriff       </td><td>192194.7             </td><td>373945.3             </td></tr>
	<tr><th scope=row>40160</th><td>Public Protection    </td><td>Senior Deputy Sheriff</td><td>189972.2             </td><td>390984.1             </td></tr>
	<tr><th scope=row>38258</th><td>Public Protection    </td><td>Sheriff's Lieutenant </td><td>188937.8             </td><td>427324.1             </td></tr>
	<tr><th scope=row>30262</th><td>Public Protection    </td><td>Deputy Sheriff       </td><td>184093.9             </td><td>368179.8             </td></tr>
	<tr><th scope=row>13453</th><td>Public Protection    </td><td>Senior Deputy Sheriff</td><td>177436.7             </td><td>371386.2             </td></tr>
	<tr><th scope=row>23970</th><td>Public Protection    </td><td>Deputy Sheriff       </td><td>170196.5             </td><td>349619.6             </td></tr>
	<tr><th scope=row>34724</th><td>Public Protection    </td><td>Deputy Sheriff       </td><td>163724.4             </td><td>346018.1             </td></tr>
	<tr><th scope=row>34927</th><td>Public Protection    </td><td>Senior Deputy Sheriff</td><td>160622.8             </td><td>345817.9             </td></tr>
</tbody>
</table>



### - Obviously in this rank, Public Protection is the hardest work in 2017 because the salary of this kind of job is not high and employee still need to work overtime to protect the society.

# d. Salaries Rank


```R
Tcops_2017S <- select (Tcops_2017, Organization.Group,Job, Salaries ,Total.Compensation)
        head(Tcops_2017S[order(Tcops_2017S$Salaries, decreasing = T),] , n=10)
```


<table>
<thead><tr><th></th><th scope=col>Organization.Group</th><th scope=col>Job</th><th scope=col>Salaries</th><th scope=col>Total.Compensation</th></tr></thead>
<tbody>
	<tr><th scope=row>16694</th><td><span style=white-space:pre-wrap>General Administration &amp; Finance       </span></td><td><span style=white-space:pre-wrap>Chief Investment Officer                </span>   </td><td>533985.9                                                                           </td><td>668412.4                                                                           </td></tr>
	<tr><th scope=row>33877</th><td><span style=white-space:pre-wrap>General Administration &amp; Finance       </span></td><td><span style=white-space:pre-wrap>Managing Director                       </span>   </td><td>420076.6                                                                           </td><td>532690.6                                                                           </td></tr>
	<tr><th scope=row>40344</th><td>Community Health                        </td><td>Physician Administrator, DPH            </td><td>418016.6                                </td><td>538791.7                                </td></tr>
	<tr><th scope=row>9459</th><td>Public Works, Transportation &amp; Commerce                                     </td><td><span style=white-space:pre-wrap>Transit Operator                        </span></td><td>355340.6                                                                        </td><td>479167.2                                                                        </td></tr>
	<tr><th scope=row>10158</th><td><span style=white-space:pre-wrap>General Administration &amp; Finance       </span></td><td><span style=white-space:pre-wrap>Dept Head V                             </span>   </td><td>346944.0                                                                           </td><td>452385.2                                                                           </td></tr>
	<tr><th scope=row>29056</th><td>Public Works, Transportation &amp; Commerce                                     </td><td><span style=white-space:pre-wrap>Executive Contract Employee             </span></td><td>340344.0                                                                        </td><td>436449.8                                                                        </td></tr>
	<tr><th scope=row>5744</th><td>Community Health                        </td><td>Dept Head V                             </td><td>329470.3                                </td><td>424592.3                                </td></tr>
	<tr><th scope=row>35149</th><td>Public Works, Transportation &amp; Commerce                                     </td><td><span style=white-space:pre-wrap>Gen Mgr, Public Trnsp Dept              </span></td><td>324064.9                                                                        </td><td>425119.9                                                                        </td></tr>
	<tr><th scope=row>26522</th><td><span style=white-space:pre-wrap>General Administration &amp; Finance       </span></td><td><span style=white-space:pre-wrap>Managing Director                       </span>   </td><td>320644.3                                                                           </td><td>427395.4                                                                           </td></tr>
	<tr><th scope=row>15127</th><td>Community Health                        </td><td>Administrator, Department Of Public Heal</td><td>316781.3                                </td><td>408262.4                                </td></tr>
</tbody>
</table>



### - The job Chief Investment Officer and Managing Director both from the General Administration & Finance  have a good salaries in 2017. We can say if people want to find a job with a good salary, we will recommand the job from General Administration & Finance.

# e. None overtime Job Rank in 2017


```R
NOvertime_2017 <- cops %>% filter(Year == "2017", Overtime == "0")
Novertime_2017 <- select (NOvertime_2017, Organization.Group,Job, Salaries ,Total.Compensation)
        head(Tcops_2017S[order(Tcops_2017S$Total.Compensation, decreasing = T),] , n=25)
```


<table>
<thead><tr><th></th><th scope=col>Organization.Group</th><th scope=col>Job</th><th scope=col>Salaries</th><th scope=col>Total.Compensation</th></tr></thead>
<tbody>
	<tr><th scope=row>16694</th><td><span style=white-space:pre-wrap>General Administration &amp; Finance        </span></td><td><span style=white-space:pre-wrap>Chief Investment Officer                </span>    </td><td>533985.9                                                                            </td><td>668412.4                                                                            </td></tr>
	<tr><th scope=row>40344</th><td>Community Health                        </td><td>Physician Administrator, DPH            </td><td>418016.6                                </td><td>538791.7                                </td></tr>
	<tr><th scope=row>33877</th><td><span style=white-space:pre-wrap>General Administration &amp; Finance        </span></td><td><span style=white-space:pre-wrap>Managing Director                       </span>    </td><td>420076.6                                                                            </td><td>532690.6                                                                            </td></tr>
	<tr><th scope=row>9459</th><td>Public Works, Transportation &amp; Commerce                                     </td><td><span style=white-space:pre-wrap>Transit Operator                        </span></td><td>355340.6                                                                        </td><td>479167.2                                                                        </td></tr>
	<tr><th scope=row>10158</th><td><span style=white-space:pre-wrap>General Administration &amp; Finance        </span></td><td><span style=white-space:pre-wrap>Dept Head V                             </span>    </td><td>346944.0                                                                            </td><td>452385.2                                                                            </td></tr>
	<tr><th scope=row>39784</th><td>Public Protection                       </td><td>Chief, Fire Department                  </td><td>312390.9                                </td><td>443297.1                                </td></tr>
	<tr><th scope=row>36917</th><td>Community Health                        </td><td>Senior Physician Specialist             </td><td>243095.4                                </td><td>436540.5                                </td></tr>
	<tr><th scope=row>29056</th><td>Public Works, Transportation &amp; Commerce                                     </td><td><span style=white-space:pre-wrap>Executive Contract Employee             </span></td><td>340344.0                                                                        </td><td>436449.8                                                                        </td></tr>
	<tr><th scope=row>26522</th><td><span style=white-space:pre-wrap>General Administration &amp; Finance        </span></td><td><span style=white-space:pre-wrap>Managing Director                       </span>    </td><td>320644.3                                                                            </td><td>427395.4                                                                            </td></tr>
	<tr><th scope=row>38258</th><td>Public Protection                       </td><td>Sheriff's Lieutenant                    </td><td>138857.5                                </td><td>427324.1                                </td></tr>
	<tr><th scope=row>35149</th><td>Public Works, Transportation &amp; Commerce                                     </td><td><span style=white-space:pre-wrap>Gen Mgr, Public Trnsp Dept              </span></td><td>324064.9                                                                        </td><td>425119.9                                                                        </td></tr>
	<tr><th scope=row>5744</th><td>Community Health                        </td><td>Dept Head V                             </td><td>329470.3                                </td><td>424592.3                                </td></tr>
	<tr><th scope=row>37783</th><td><span style=white-space:pre-wrap>General Administration &amp; Finance        </span></td><td><span style=white-space:pre-wrap>Asst Med Examiner                       </span>    </td><td>297044.2                                                                            </td><td>412734.4                                                                            </td></tr>
	<tr><th scope=row>37635</th><td>Public Protection                       </td><td>Asst Chf Of Dept (Fire Dept)            </td><td>211664.3                                </td><td>408931.9                                </td></tr>
	<tr><th scope=row>2592</th><td>Community Health                        </td><td>Manager VIII                            </td><td>310140.0                                </td><td>408570.0                                </td></tr>
	<tr><th scope=row>15127</th><td>Community Health                        </td><td>Administrator, Department Of Public Heal</td><td>316781.3                                </td><td>408262.4                                </td></tr>
	<tr><th scope=row>7482</th><td>Public Works, Transportation &amp; Commerce                                     </td><td><span style=white-space:pre-wrap>Dept Head V                             </span></td><td>308965.2                                                                        </td><td>398404.8                                                                        </td></tr>
	<tr><th scope=row>29002</th><td><span style=white-space:pre-wrap>General Administration &amp; Finance        </span></td><td><span style=white-space:pre-wrap>Dept Head V                             </span>    </td><td>299339.7                                                                            </td><td>395618.9                                                                            </td></tr>
	<tr><th scope=row>42289</th><td>Public Protection                       </td><td>Deputy Sheriff                          </td><td>104621.0                                </td><td>393669.9                                </td></tr>
	<tr><th scope=row>31073</th><td><span style=white-space:pre-wrap>General Administration &amp; Finance        </span></td><td><span style=white-space:pre-wrap>Mayor                                   </span>    </td><td>303563.1                                                                            </td><td>392829.7                                                                            </td></tr>
	<tr><th scope=row>40160</th><td>Public Protection                       </td><td>Senior Deputy Sheriff                   </td><td>116405.9                                </td><td>390984.1                                </td></tr>
	<tr><th scope=row>25960</th><td>Public Protection                       </td><td>Battlion Chief, Fire Suppressi          </td><td>184897.1                                </td><td>390412.0                                </td></tr>
	<tr><th scope=row>17893</th><td>Public Protection                       </td><td>Battlion Chief, Fire Suppressi          </td><td>199080.5                                </td><td>387981.3                                </td></tr>
	<tr><th scope=row>11861</th><td>Human Welfare &amp; Neighborhood Development                                    </td><td><span style=white-space:pre-wrap>Dept Head V                             </span></td><td>299287.8                                                                        </td><td>387314.7                                                                        </td></tr>
	<tr><th scope=row>37897</th><td>Public Protection                       </td><td>Deputy Sheriff                          </td><td>105023.3                                </td><td>386896.9                                </td></tr>
</tbody>
</table>




```R
CNOvertime <- cops %>% filter(Overtime == "0") %>% group_by (Year) %>% summarize (num_Novertime = n())
qplot(Year, num_Novertime, data = CNOvertime,
     geom = c("line"))
```




![png](output_47_1.png)


### - None overtime rank shows that in some position, employee barely have to work overtime, and also we get the rank that allow us to know which job without overtime still has a good Salaries. It may guide people to consider.
### In addition, in the line chart, we can see there is more none-overtime job than the past. It seems government is improving the situation of overtime. People also have more consideration of none- overtime job. 

# 5. Compare Public Protection and General Administration & Finance

## a. Public Protection Pie Chart

### - // Using filter function to get the data in 2017 and get the jobs in Organization Group. Using mean function to get the average of each column, and make a data frame called P_ave_pie. By using ggplot function to draw the pie chart.


```R
PublicProtect <- cops %>% filter(Year == "2017" , Organization.Group =="Public Protection" )

P_ave_TC <- mean(PublicProtect$Total.Compensation)
P_ave_S <- mean(PublicProtect$Salaries)
P_ave_O <- mean(PublicProtect$Overtime)
P_ave_OS <- mean(PublicProtect$Other.Salaries)
P_ave_R <- mean(PublicProtect$Retirement)
P_ave_HD <- mean(PublicProtect$Health.Dental)
P_ave_OB <- mean(PublicProtect$Other.Benefits)

P_ave_pie <- data.frame(P_ave_TC = c("Salaries", "Overtime", "Other.Salaries", 
                                 "Retirement", "Health.Dental","Other.Benefits"),
                      P_perc=c(P_ave_S,P_ave_O,P_ave_OS,P_ave_R,P_ave_HD,P_ave_OB))
                 P_ave_pie = P_ave_pie[order(P_ave_pie$P_perc, decreasing = TRUE),] 
                     myLabel = as.vector(P_ave_pie$P_ave_TC)   
                    myLabel = paste(myLabel, "(", round(P_ave_pie$P_perc / sum(P_ave_pie$P_perc) * 100, 2), " %) ", sep = "")   
                      
                 
ggplot((data=P_ave_pie),aes(x=factor(1), y=P_perc, fill=P_ave_TC)) +
    geom_bar(stat = "identity", width = 1 ) +
    coord_polar("y") +
    labs(x = "", y = "", title = "Public Protection Pie Chart") +
    theme(legend.title = element_blank(), legend.position = "top")+
    theme(axis.text.x = element_blank())  +
    scale_fill_discrete(breaks = P_ave_pie$P_ave_TC, labels = myLabel)+
    geom_text(x = 0, y = 0, label = "Salaries", alpha = 0.2)+
    geom_text(x = 0.3, y = 5, label = "Retirement                                                                      ", alpha = 0.2)+
    geom_text(x = 0.75, y = 40, label = "Overtime                                                                                         ", alpha = 0.2)+
    geom_text(x = 1.2, y = 50, label = "Other.Salaries                                                                                                     ", alpha = 0.2)+
    geom_text(x = 1.4, y =0, label = "Other Benefits                                                                                       ", alpha = 0.2)+
    geom_text(x = 1.5, y = 20, label = "Health.Dental                                      ", alpha = 0.2)
 


```




![png](output_52_1.png)


## b.General Administration & Finance Pie Chart


```R
GAF <- cops %>% filter(Year == "2017" , Organization.Group =="General Administration & Finance" )
GAF_ave_TC <- mean(GAF$Total.Compensation)
GAF_ave_S <- mean(GAF$Salaries)
GAF_ave_O <- mean(GAF$Overtime)
GAF_ave_OS <- mean(GAF$Other.Salaries)
GAF_ave_R <- mean(GAF$Retirement)
GAF_ave_HD <- mean(GAF$Health.Dental)
GAF_ave_OB <- mean(GAF$Other.Benefits)

GAF_ave_pie <- data.frame(GAF_ave_TC = c("Salaries", "Overtime", "Other.Salaries", 
                                 "Retirement", "Health.Dental","Other.Benefits"),
                      GAF_perc=c(GAF_ave_S,GAF_ave_O,GAF_ave_OS,GAF_ave_R,GAF_ave_HD,GAF_ave_OB))
                 GAF_ave_pie = GAF_ave_pie[order(GAF_ave_pie$GAF_perc, decreasing = TRUE),] 
                     myLabel = as.vector(GAF_ave_pie$GAF_ave_TC)
                    myLabel = paste(myLabel, "(", round(GAF_ave_pie$GAF_perc / sum(GAF_ave_pie$GAF_perc) * 100, 2), " %) ", sep = "")                       
                 
ggplot((data=GAF_ave_pie),aes(x=factor(1), y=GAF_perc, fill=GAF_ave_TC)) +
    geom_bar(stat = "identity", width = 1 ) +
    coord_polar("y") +
    labs(x = "", y = "", title = "General Administration & Finance Pie Chart") +
    theme(legend.title = element_blank(), legend.position = "top")+
    theme(axis.text.x = element_blank())  +
    scale_fill_discrete(breaks = GAF_ave_pie$GAF_ave_TC, labels = myLabel)+
    geom_text(x = 0, y = 0, label = "Salaries", alpha = 0.2)+
    geom_text(x = 0.5, y = 5, label = "Retirement                                                                      ", alpha = 0.2)+
    geom_text(x = 0.9, y = 40, label = "Overtime                                                                                         ", alpha = 0.2)+
    geom_text(x = 1.0, y = 50, label = "Other.Salaries                                                                                                     ", alpha = 0.2)+
    geom_text(x = 1.2, y =0, label = "Other Benefits                                                                                       ", alpha = 0.2)+
    geom_text(x = 1.5, y = 20, label = "Health.Dental                                      ", alpha = 0.2)
 



```




![png](output_54_1.png)


### - As this two chart, we know the jobs of Public Protection have around 9.2% overtime and the jobs of General Administration & Finance have only 1.05% overtime. So, it mean Public Protection jobs is more exhausting.

# For Advanced Level


```R
FAL <- cops %>% filter(Job == "Firefighter")

FALS <- select (FAL, Year ,Job, Retirement)

head(FALS[order(FALS$Retirement, decreasing = T),] , n=25)

qplot(Year,Retirement, data = FALS,
geom = c("point", "line"))
```


<table>
<thead><tr><th></th><th scope=col>Year</th><th scope=col>Job</th><th scope=col>Retirement</th></tr></thead>
<tbody>
	<tr><th scope=row>2881</th><td>2015       </td><td>Firefighter</td><td>35397.88   </td></tr>
	<tr><th scope=row>2505</th><td>2015       </td><td>Firefighter</td><td>32606.06   </td></tr>
	<tr><th scope=row>2169</th><td>2015       </td><td>Firefighter</td><td>32534.11   </td></tr>
	<tr><th scope=row>3670</th><td>2015       </td><td>Firefighter</td><td>32065.52   </td></tr>
	<tr><th scope=row>2506</th><td>2015       </td><td>Firefighter</td><td>31529.17   </td></tr>
	<tr><th scope=row>2381</th><td>2015       </td><td>Firefighter</td><td>31402.59   </td></tr>
	<tr><th scope=row>2711</th><td>2014       </td><td>Firefighter</td><td>31113.59   </td></tr>
	<tr><th scope=row>272</th><td>2014       </td><td>Firefighter</td><td>30883.26   </td></tr>
	<tr><th scope=row>618</th><td>2015       </td><td>Firefighter</td><td>30467.33   </td></tr>
	<tr><th scope=row>3802</th><td>2015       </td><td>Firefighter</td><td>30312.20   </td></tr>
	<tr><th scope=row>870</th><td>2015       </td><td>Firefighter</td><td>30139.41   </td></tr>
	<tr><th scope=row>3342</th><td>2015       </td><td>Firefighter</td><td>30114.69   </td></tr>
	<tr><th scope=row>2969</th><td>2015       </td><td>Firefighter</td><td>30037.79   </td></tr>
	<tr><th scope=row>4188</th><td>2015       </td><td>Firefighter</td><td>29968.31   </td></tr>
	<tr><th scope=row>2853</th><td>2015       </td><td>Firefighter</td><td>29834.85   </td></tr>
	<tr><th scope=row>1789</th><td>2015       </td><td>Firefighter</td><td>29797.13   </td></tr>
	<tr><th scope=row>3521</th><td>2015       </td><td>Firefighter</td><td>29778.94   </td></tr>
	<tr><th scope=row>3917</th><td>2014       </td><td>Firefighter</td><td>29774.99   </td></tr>
	<tr><th scope=row>1501</th><td>2015       </td><td>Firefighter</td><td>29762.87   </td></tr>
	<tr><th scope=row>1248</th><td>2015       </td><td>Firefighter</td><td>29760.07   </td></tr>
	<tr><th scope=row>3882</th><td>2014       </td><td>Firefighter</td><td>29716.36   </td></tr>
	<tr><th scope=row>1381</th><td>2015       </td><td>Firefighter</td><td>29484.71   </td></tr>
	<tr><th scope=row>1444</th><td>2015       </td><td>Firefighter</td><td>29398.88   </td></tr>
	<tr><th scope=row>1041</th><td>2015       </td><td>Firefighter</td><td>29382.54   </td></tr>
	<tr><th scope=row>3204</th><td>2015       </td><td>Firefighter</td><td>29341.04   </td></tr>
</tbody>
</table>






![png](output_57_2.png)


### - This chart can provide the tendency of the retirement of compensation of firefighter. we can see in here the retirement compensation is decreasing. In 2017, the number is around 22000, but according the recording, in 2015, it was the highest number of retirement compensation. So, when the CEO is considering about retirement for firefighter, this data will helpful to improve it appropriately.

# -Summary- 

### We analyzed the structure of compensation. The result shows that the percentage of each elements are not too much changed from 2013 to 2017 in general. 
### In pie chart, Salaries takes up the most of part, Retirement is second, and Health/Dental is third. Then, we compare the total compensation change in each job in each year with ranking.
### It shows that the publication protect was the highest, but in 2015 Chief Investment Officer  was becoming higher than the publication protect until 2017. 
### We explored in specific data: Chief Of Police and Chief Investment Officer. The salaries of chief investment officer is higher than chief of police. So, we analyzed the advantage in the different jobs with different conditions. we find the most overtime and health/dental job is belonging to public protection. 
### We also look for none overtime job with good salaries. In final, we show the data that working in General Administration & Finance area is may a good choise.

# -Recommandation-

### This recommandation for San Francisco Chronicle newspaper CEO is to show the fact of job. 
### The jobs in public protection is good for the person who want to help to maintain the security. It will be a pretty great dream job. But, this job's basic salaries is not too hight. They are leaning on overtime pay.  
### for the person who is thinking about overtime, I will recommand the job in General Administration & Finance area. 
### According to the data above, it barely need to work overtime and the salaries is good. we also have a investigation of none overtime job. 
### There may some people want to apply this kind of job. we have top three to recommand: In General Administration & Finance, Chief Investment Officer, In Community Health, Physician Administrator, and also in General Administration & Finance, Managing Director. 
### In this report, there may some data are miss that may cause the average is not accurate, but we still tried our best to show the useful truth to people. 
### So, I will recommand to attract the attention from government to take care of the public protection group. This is because this job salaries is decreaing now. 


```R

```
