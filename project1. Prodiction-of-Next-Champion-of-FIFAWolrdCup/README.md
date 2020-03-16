# ============== Soccer: Live it and Love it ===================
## Analyzed by Marco Lin

![](http://www.blogproductreview.com/wp-content/uploads/2018/10/download-6.jpeg)

 # ===========Objective of the Proposed Research==============

#### - The FIFA World Cup is the biggest single-event sporting competition in the world. And, FIFA 19 is a football simulation video game developed by EA Vancouver as part of Electronic Arts' FIFA series. The company which made this game hold an event call soccer: live it and love it. Because this data base on the real players data. And they want a comprehensive analysis report to predict which team will be the champions, analyze the correlation between different position and skill and recommend a dream team for them. 

#### we will start our analysis from cleaning the data because the columns "Club"," Club logo", "Photo", "Flag", "Loaned. From", "Real face", and "Body type","Height", "Weight” are not used in our analysis. especially, in this data we have many detail data about physical ability, so the height and the weight can be ignored. 

#### Then, we will analyze from Overall score and potential score to each position score for the different purpose. For a golden ball award winner, we will focus on "ST","CB","GK", and "CAM" and compare these with the score of server ability score. for team prediction, we will focus on the average of the ability in each country. The champion team needs a good balance between each teammate. At final, there will be a summary and recommendation for FIFA.

# 1.) =================== Preparation===================


```R
FIFA <- read.csv("~/project-ionic/R/project/data.csv")
```


```R
FIFA$Height_cm <-as.character(FIFA$Height_cm)
```


```R
FIFA$Height_cm <-as.numeric(FIFA$Height_cm)
```

    Warning message in eval(expr, envir, enclos):
    “強制變更過程中產生了 NA”


```R
FIFA$Weight_kg <-as.character(FIFA$Weight_kg)
```


```R
FIFA$Weight_kg <-as.numeric(FIFA$Weight_kg)
```

    Warning message in eval(expr, envir, enclos):
    “強制變更過程中產生了 NA”


```R
FIFA$potential_value <-as.character(FIFA$potential_value)
```


```R
FIFA$potential_value <-as.numeric(FIFA$potential_value)
```

    Warning message in eval(expr, envir, enclos):
    “強制變更過程中產生了 NA”


```R
FIFA$Position <- as.character(FIFA$Position)
```


```R
library(tidyverse)
```

    ─ Attaching packages ──────────────────── tidyverse 1.2.1 ─
    ✔ ggplot2 3.0.0     ✔ purrr   0.2.5
    ✔ tibble  1.4.2     ✔ dplyr   0.7.6
    ✔ tidyr   0.8.1     ✔ stringr 1.3.1
    ✔ readr   1.1.1     ✔ forcats 0.3.0
    ─ Conflicts ───────────────────── tidyverse_conflicts() ─
    ✖ dplyr::filter() masks stats::filter()
    ✖ dplyr::lag()    masks stats::lag()



```R
library(psych)
```

    
    Attaching package: ‘psych’
    
    The following objects are masked from ‘package:ggplot2’:
    
        %+%, alpha
    


# 2.)==================Data Exploration====================

## 2.a )  AGE and Players Correlation


```R
names(FIFA)
```


<ol class=list-inline>
	<li>'X'</li>
	<li>'ID'</li>
	<li>'Name'</li>
	<li>'Age'</li>
	<li>'Photo'</li>
	<li>'Nationality'</li>
	<li>'Flag'</li>
	<li>'Overall'</li>
	<li>'Potential'</li>
	<li>'Club'</li>
	<li>'Club.Logo'</li>
	<li>'potential_value'</li>
	<li>'Value'</li>
	<li>'Salary'</li>
	<li>'Wage'</li>
	<li>'Special'</li>
	<li>'Preferred.Foot'</li>
	<li>'International.Reputation'</li>
	<li>'Weak.Foot'</li>
	<li>'Skill.Moves'</li>
	<li>'Work.Rate'</li>
	<li>'Body.Type'</li>
	<li>'Real.Face'</li>
	<li>'Position'</li>
	<li>'Jersey.Number'</li>
	<li>'Joined'</li>
	<li>'Loaned.From'</li>
	<li>'Contract.Valid.Until'</li>
	<li>'feet'</li>
	<li>'inch'</li>
	<li>'Height_cm'</li>
	<li>'Height'</li>
	<li>'Weight_kg'</li>
	<li>'Weight'</li>
	<li>'LS'</li>
	<li>'ST'</li>
	<li>'RS'</li>
	<li>'LW'</li>
	<li>'LF'</li>
	<li>'CF'</li>
	<li>'RF'</li>
	<li>'RW'</li>
	<li>'LAM'</li>
	<li>'CAM'</li>
	<li>'RAM'</li>
	<li>'LM'</li>
	<li>'LCM'</li>
	<li>'CM'</li>
	<li>'RCM'</li>
	<li>'RM'</li>
	<li>'LWB'</li>
	<li>'LDM'</li>
	<li>'CDM'</li>
	<li>'RDM'</li>
	<li>'RWB'</li>
	<li>'LB'</li>
	<li>'LCB'</li>
	<li>'CB'</li>
	<li>'RCB'</li>
	<li>'RB'</li>
	<li>'Crossing'</li>
	<li>'Finishing'</li>
	<li>'HeadingAccuracy'</li>
	<li>'ShortPassing'</li>
	<li>'Volleys'</li>
	<li>'Dribbling'</li>
	<li>'Curve'</li>
	<li>'FKAccuracy'</li>
	<li>'LongPassing'</li>
	<li>'BallControl'</li>
	<li>'Acceleration'</li>
	<li>'SprintSpeed'</li>
	<li>'Agility'</li>
	<li>'Reactions'</li>
	<li>'Balance'</li>
	<li>'ShotPower'</li>
	<li>'Jumping'</li>
	<li>'Stamina'</li>
	<li>'Strength'</li>
	<li>'LongShots'</li>
	<li>'Aggression'</li>
	<li>'Interceptions'</li>
	<li>'Positioning'</li>
	<li>'Vision'</li>
	<li>'Penalties'</li>
	<li>'Composure'</li>
	<li>'Marking'</li>
	<li>'StandingTackle'</li>
	<li>'SlidingTackle'</li>
	<li>'GKDiving'</li>
	<li>'GKHandling'</li>
	<li>'GKKicking'</li>
	<li>'GKPositioning'</li>
	<li>'GKReflexes'</li>
	<li>'Release.Clause'</li>
</ol>




```R
Age_FIFA <- FIFA %>% group_by (Age) %>% summarize (Num = n())

head(Age_FIFA[order(Age_FIFA$Num, decreasing = T), ], 10)

qplot(Age, Num, data = Age_FIFA,
         geom = c("line"))
```


<table>
<thead><tr><th scope=col>Age</th><th scope=col>Num</th></tr></thead>
<tbody>
	<tr><td>21  </td><td>1423</td></tr>
	<tr><td>26  </td><td>1387</td></tr>
	<tr><td>24  </td><td>1358</td></tr>
	<tr><td>22  </td><td>1340</td></tr>
	<tr><td>23  </td><td>1332</td></tr>
	<tr><td>25  </td><td>1319</td></tr>
	<tr><td>20  </td><td>1240</td></tr>
	<tr><td>27  </td><td>1162</td></tr>
	<tr><td>28  </td><td>1101</td></tr>
	<tr><td>19  </td><td>1024</td></tr>
</tbody>
</table>






![png](output_18_2.png)


## Explanation:
### The most all players' age in world cup is in the range 19~26. The highest population in the group of age is 21.  

## 2.b )  Countries and Players Correlation


```R
Nationality_FIFA <- FIFA %>% group_by (Nationality) %>% summarize (Num = n())

head(Nationality_FIFA[order(Nationality_FIFA$Num, decreasing = T), ], 10)

mean(Nationality_FIFA$Num)

ANationality_FIFA <- Nationality_FIFA %>% filter(Num >= 200)


ggplot(ANationality_FIFA) + geom_bar(stat = "identity", color = 'steelblue', 
                            aes(x = Nationality, y = Num)) + theme(axis.text.x=element_text(size=rel(1), angle=90))
```


<table>
<thead><tr><th scope=col>Nationality</th><th scope=col>Num</th></tr></thead>
<tbody>
	<tr><td>England    </td><td>1662       </td></tr>
	<tr><td>Germany    </td><td>1198       </td></tr>
	<tr><td>Spain      </td><td>1072       </td></tr>
	<tr><td>Argentina  </td><td> 937       </td></tr>
	<tr><td>France     </td><td> 914       </td></tr>
	<tr><td>Brazil     </td><td> 827       </td></tr>
	<tr><td>Italy      </td><td> 702       </td></tr>
	<tr><td>Colombia   </td><td> 618       </td></tr>
	<tr><td>Japan      </td><td> 478       </td></tr>
	<tr><td>Netherlands</td><td> 453       </td></tr>
</tbody>
</table>




111.018292682927





![png](output_21_3.png)


## Explanation:
### After, We calculate the total number of players in each country, we found the average of number is 111. So, we filter out the total number under 200. In bar chart,  it appears that the players from England, Germany, Spain, Argentina take up most of part.

## 2.c )  Preferred Foot and Players Correlation


```R
PreferredFoot_FIFA <- FIFA %>% group_by (Preferred.Foot) %>% summarize (Num = n())

foot_pie <- data.frame(foot_pie = c("Left", "Right", "None"),
                      Foot_perc=c(4211,13948,48))
                 foot_pie = foot_pie[order(foot_pie$Foot_perc, decreasing = TRUE),] 
                     myLabel = as.vector(foot_pie$foot_pie)
                    myLabel = paste(myLabel, "(", round(foot_pie$Foot_perc / sum(PreferredFoot_FIFA$Num) * 100, 2), " %) ", sep = "")                       
                 
ggplot((data=foot_pie),aes(x=factor(1), y=Foot_perc, fill=foot_pie)) +
    geom_bar(stat = "identity", width = 1 ) +
    coord_polar("y") +
    labs(x = "", y = "", title = "Preferred Foot") +
    theme(legend.title = element_blank(), legend.position = "top")+
    theme(axis.text.x = element_blank())  +
    scale_fill_discrete(breaks = foot_pie$foot_pie, labels = myLabel)+
    geom_text(x = 0, y = 0, label = "Right 76.61%", alpha = 0.2)+
    geom_text(x = 0.9, y = 40, label = "Left 23.13%                                                        ", alpha = 0.2)
```




![png](output_24_1.png)


## Explanation:
### Most all of players' preferred foot are right taking up 76%. Left players take up 23% in the pie chart.

## 2.d ) Value Rank


```R
ValueRank <- FIFA %>% select(Name, potential_value, Overall, Jersey.Number, Position) 
head(ValueRank[order(ValueRank$potential_value, decreasing = T), ], 10)

```


<table>
<thead><tr><th></th><th scope=col>Name</th><th scope=col>potential_value</th><th scope=col>Overall</th><th scope=col>Jersey.Number</th><th scope=col>Position</th></tr></thead>
<tbody>
	<tr><th scope=row>3</th><td>Neymar Jr        </td><td>118.5            </td><td>92               </td><td>10               </td><td>LW               </td></tr>
	<tr><th scope=row>1</th><td>L. Messi         </td><td>110.5            </td><td>94               </td><td>10               </td><td>RF               </td></tr>
	<tr><th scope=row>5</th><td>K. De Bruyne     </td><td>102.0            </td><td>91               </td><td> 7               </td><td>RCM              </td></tr>
	<tr><th scope=row>6</th><td>E. Hazard        </td><td> 93.0            </td><td>91               </td><td>10               </td><td>LF               </td></tr>
	<tr><th scope=row>16</th><td>P. Dybala        </td><td> 89.0            </td><td>89               </td><td>21               </td><td>LF               </td></tr>
	<tr><th scope=row>17</th><td>H. Kane          </td><td> 83.5            </td><td>89               </td><td> 9               </td><td>ST               </td></tr>
	<tr><th scope=row>26</th><td>K. Mbappé        </td><td> 81.0            </td><td>88               </td><td>10               </td><td>RM               </td></tr>
	<tr><th scope=row>8</th><td>L. Suárez        </td><td> 80.0            </td><td>91               </td><td> 9               </td><td>RS               </td></tr>
	<tr><th scope=row>18</th><td>A. Griezmann     </td><td> 78.0            </td><td>89               </td><td> 7               </td><td>CAM              </td></tr>
	<tr><th scope=row>2</th><td>Cristiano Ronaldo</td><td> 77.0            </td><td>94               </td><td> 7               </td><td>ST               </td></tr>
</tbody>
</table>



## Explanation:
### The top 5 valuest of soccer players are Neymar, Messi, Bruyne, Hazard, Dybala.


# 3.)==================Data Cleaning====================


```R
names(FIFA)
FIFA <- subset(FIFA, select = -c(Club, Club.Logo, Photo, Flag, Loaned.From, Real.Face, Body.Type, Contract.Valid.Until, Release.Clause, Height,Weight))
names(FIFA)
```


<ol class=list-inline>
	<li>'X'</li>
	<li>'ID'</li>
	<li>'Name'</li>
	<li>'Age'</li>
	<li>'Photo'</li>
	<li>'Nationality'</li>
	<li>'Flag'</li>
	<li>'Overall'</li>
	<li>'Potential'</li>
	<li>'Club'</li>
	<li>'Club.Logo'</li>
	<li>'potential_value'</li>
	<li>'Value'</li>
	<li>'Salary'</li>
	<li>'Wage'</li>
	<li>'Special'</li>
	<li>'Preferred.Foot'</li>
	<li>'International.Reputation'</li>
	<li>'Weak.Foot'</li>
	<li>'Skill.Moves'</li>
	<li>'Work.Rate'</li>
	<li>'Body.Type'</li>
	<li>'Real.Face'</li>
	<li>'Position'</li>
	<li>'Jersey.Number'</li>
	<li>'Joined'</li>
	<li>'Loaned.From'</li>
	<li>'Contract.Valid.Until'</li>
	<li>'feet'</li>
	<li>'inch'</li>
	<li>'Height_cm'</li>
	<li>'Height'</li>
	<li>'Weight_kg'</li>
	<li>'Weight'</li>
	<li>'LS'</li>
	<li>'ST'</li>
	<li>'RS'</li>
	<li>'LW'</li>
	<li>'LF'</li>
	<li>'CF'</li>
	<li>'RF'</li>
	<li>'RW'</li>
	<li>'LAM'</li>
	<li>'CAM'</li>
	<li>'RAM'</li>
	<li>'LM'</li>
	<li>'LCM'</li>
	<li>'CM'</li>
	<li>'RCM'</li>
	<li>'RM'</li>
	<li>'LWB'</li>
	<li>'LDM'</li>
	<li>'CDM'</li>
	<li>'RDM'</li>
	<li>'RWB'</li>
	<li>'LB'</li>
	<li>'LCB'</li>
	<li>'CB'</li>
	<li>'RCB'</li>
	<li>'RB'</li>
	<li>'Crossing'</li>
	<li>'Finishing'</li>
	<li>'HeadingAccuracy'</li>
	<li>'ShortPassing'</li>
	<li>'Volleys'</li>
	<li>'Dribbling'</li>
	<li>'Curve'</li>
	<li>'FKAccuracy'</li>
	<li>'LongPassing'</li>
	<li>'BallControl'</li>
	<li>'Acceleration'</li>
	<li>'SprintSpeed'</li>
	<li>'Agility'</li>
	<li>'Reactions'</li>
	<li>'Balance'</li>
	<li>'ShotPower'</li>
	<li>'Jumping'</li>
	<li>'Stamina'</li>
	<li>'Strength'</li>
	<li>'LongShots'</li>
	<li>'Aggression'</li>
	<li>'Interceptions'</li>
	<li>'Positioning'</li>
	<li>'Vision'</li>
	<li>'Penalties'</li>
	<li>'Composure'</li>
	<li>'Marking'</li>
	<li>'StandingTackle'</li>
	<li>'SlidingTackle'</li>
	<li>'GKDiving'</li>
	<li>'GKHandling'</li>
	<li>'GKKicking'</li>
	<li>'GKPositioning'</li>
	<li>'GKReflexes'</li>
	<li>'Release.Clause'</li>
</ol>




<ol class=list-inline>
	<li>'X'</li>
	<li>'ID'</li>
	<li>'Name'</li>
	<li>'Age'</li>
	<li>'Nationality'</li>
	<li>'Overall'</li>
	<li>'Potential'</li>
	<li>'potential_value'</li>
	<li>'Value'</li>
	<li>'Salary'</li>
	<li>'Wage'</li>
	<li>'Special'</li>
	<li>'Preferred.Foot'</li>
	<li>'International.Reputation'</li>
	<li>'Weak.Foot'</li>
	<li>'Skill.Moves'</li>
	<li>'Work.Rate'</li>
	<li>'Position'</li>
	<li>'Jersey.Number'</li>
	<li>'Joined'</li>
	<li>'feet'</li>
	<li>'inch'</li>
	<li>'Height_cm'</li>
	<li>'Weight_kg'</li>
	<li>'LS'</li>
	<li>'ST'</li>
	<li>'RS'</li>
	<li>'LW'</li>
	<li>'LF'</li>
	<li>'CF'</li>
	<li>'RF'</li>
	<li>'RW'</li>
	<li>'LAM'</li>
	<li>'CAM'</li>
	<li>'RAM'</li>
	<li>'LM'</li>
	<li>'LCM'</li>
	<li>'CM'</li>
	<li>'RCM'</li>
	<li>'RM'</li>
	<li>'LWB'</li>
	<li>'LDM'</li>
	<li>'CDM'</li>
	<li>'RDM'</li>
	<li>'RWB'</li>
	<li>'LB'</li>
	<li>'LCB'</li>
	<li>'CB'</li>
	<li>'RCB'</li>
	<li>'RB'</li>
	<li>'Crossing'</li>
	<li>'Finishing'</li>
	<li>'HeadingAccuracy'</li>
	<li>'ShortPassing'</li>
	<li>'Volleys'</li>
	<li>'Dribbling'</li>
	<li>'Curve'</li>
	<li>'FKAccuracy'</li>
	<li>'LongPassing'</li>
	<li>'BallControl'</li>
	<li>'Acceleration'</li>
	<li>'SprintSpeed'</li>
	<li>'Agility'</li>
	<li>'Reactions'</li>
	<li>'Balance'</li>
	<li>'ShotPower'</li>
	<li>'Jumping'</li>
	<li>'Stamina'</li>
	<li>'Strength'</li>
	<li>'LongShots'</li>
	<li>'Aggression'</li>
	<li>'Interceptions'</li>
	<li>'Positioning'</li>
	<li>'Vision'</li>
	<li>'Penalties'</li>
	<li>'Composure'</li>
	<li>'Marking'</li>
	<li>'StandingTackle'</li>
	<li>'SlidingTackle'</li>
	<li>'GKDiving'</li>
	<li>'GKHandling'</li>
	<li>'GKKicking'</li>
	<li>'GKPositioning'</li>
	<li>'GKReflexes'</li>
</ol>



## Explanation:
### I clean the columns: "Club","Club logo","Photo","Flag","Loaned.From","Realface",and "Bodytype" which are not useful for our analysis.

# 4.)===================Adaptation====================


```R
FIFA<-within(FIFA,{ Score<- as.integer(Potential)-as.integer(Overall)})

FIFA_Score <- select(FIFA, Name, Potential, Overall, Score, Age)
head(FIFA_Score[order(FIFA_Score$Score, decreasing = T), ], 10)
```


<table>
<thead><tr><th></th><th scope=col>Name</th><th scope=col>Potential</th><th scope=col>Overall</th><th scope=col>Score</th><th scope=col>Age</th></tr></thead>
<tbody>
	<tr><th scope=row>16029</th><td>J. von Moos  </td><td>84           </td><td>58           </td><td>26           </td><td>17           </td></tr>
	<tr><th scope=row>18073</th><td>D. Campbell  </td><td>76           </td><td>50           </td><td>26           </td><td>17           </td></tr>
	<tr><th scope=row>16630</th><td>Y. Lenze     </td><td>82           </td><td>57           </td><td>25           </td><td>17           </td></tr>
	<tr><th scope=row>17176</th><td>B. Mumba     </td><td>80           </td><td>55           </td><td>25           </td><td>16           </td></tr>
	<tr><th scope=row>17785</th><td>K. Askildsen </td><td>77           </td><td>52           </td><td>25           </td><td>17           </td></tr>
	<tr><th scope=row>13928</th><td>A. Dabo      </td><td>86           </td><td>62           </td><td>24           </td><td>17           </td></tr>
	<tr><th scope=row>15729</th><td>G. Azzinnari </td><td>83           </td><td>59           </td><td>24           </td><td>17           </td></tr>
	<tr><th scope=row>16817</th><td>I. Sauter    </td><td>80           </td><td>56           </td><td>24           </td><td>17           </td></tr>
	<tr><th scope=row>18045</th><td>K. Lara      </td><td>74           </td><td>50           </td><td>24           </td><td>16           </td></tr>
	<tr><th scope=row>18051</th><td>E. Destanoglu</td><td>74           </td><td>50           </td><td>24           </td><td>17           </td></tr>
</tbody>
</table>



## Explanation:
### We have create a Score column which is made by potencial score cut overall score that allows us to understand the possibility of each player easily. And, we found the player who has highest score is J. von Moos. It appears that the score has correlation with age.
![](https://images.performgroup.com/di/library/GOAL/ef/9c/julian-von-moos-fc-basel_s4184pkw7bf613yl6xd2ic0n6.jpg?t=1748081686)

# ===================Best Squared===========================

# 4-3-3 formation
### This formation is most common formation in soccer games. So, my analysis foucus on this formation.

![](https://www.thoughtco.com/thmb/hAZomoxXf7I44B9BSZrk3-GNQII=/600x849/filters:fill(auto,1)/Association_football_4_3_3_formation-588fc84e5f9b5874ee616671.jpg)

### list of abbreviations of Soccer position.

### Defensive: 
#### GK = Goalkeeper 
#### SW = Sweeper 
#### RWB = Right Wing Back 
#### RB = Right back
#### RCB = Right center back 
#### CB = Center back
#### LCB = Left center back 
#### LB = Left back 
#### LWB = Left Wing Back 

### Midfielders:
#### RDM = Right defensive midfield
#### RCDM = Right center defensive midfield
#### CDM = Center defensive midfield
#### LCDM = Left center defensive midfield
#### LDM = Left defensive midfield
#### RWM = Right Wing Midfield
#### RM = Right midfield
#### RCM = Right center midfield 
#### CM = Center Midfield 
#### LCM = Left center midfield 
#### LM = Left midfield 
#### LWM = Left Wing Midfield
#### RAM = Right attacking midfield
#### RCAM = Right center attacking midfield
#### CAM = Center attacking midfield
#### LCAM = Left center attacking midfield
#### LAM = Left attacking midfield

### Forwards:
#### RF = Right forward
#### CF = Center forward
#### LF = Left forward
#### RS = Right Striker
#### ST = Striker
#### LS = Left Striker

### In this formation, we need a GK, a ST, a (LS or LW or LF), a (RS or RW or RF) in defensive position, a RAM, a LAM, a CM, a RWB, a LWB, CB. 

## Explanation: I sperated the position into different part of formation to calculate the average of score in each position.


```R
#GOALKeep

GoalKeeper_position<- FIFA %>% filter(Position == "GK") %>% 
select (Name, Nationality, Overall, Score, Position)
head(GoalKeeper_position)

#forward_position
forward_position<- FIFA %>% filter(Position == "LS" | Position == "RS" | Position == "LW" | Position == "RW" |  
                          Position == "ST" |  Position == "LF" |  Position == "RF" |  Position == "CF") %>% 
select (Name, Nationality, Overall, Score, Position)
head(forward_position[order(forward_position$Overall, decreasing = T), ],10)


#Midfield_position
Midfield_position<- FIFA %>% filter( Position == "RAM" | Position == "LCM" | Position == "RCM" |
                          Position == "RM" |  Position == "LM" |  Position == "CM" |  Position == "CAM" |  
                                    Position == "LDM" | Position == "CDM" |  Position == "RDM")  %>% 
select (Name, Nationality, Overall, Score, Position)
head(Midfield_position[order(Midfield_position$Overall, decreasing = T), ],10)


#Back_position
Back_position<- FIFA %>% filter(Position == "LWB" | Position == "RWB" | Position == "CB" | Position == "RCB" |  
                          Position == "LCB" |  Position == "LB" |  Position == "RB") %>% 
select (Name, Nationality, Overall, Score, Position)

head(Back_position[order(Back_position$Overall, decreasing = T), ],10)
```


<table>
<thead><tr><th scope=col>Name</th><th scope=col>Nationality</th><th scope=col>Overall</th><th scope=col>Score</th><th scope=col>Position</th></tr></thead>
<tbody>
	<tr><td>De Gea       </td><td>Spain        </td><td>91           </td><td>2            </td><td>GK           </td></tr>
	<tr><td>J. Oblak     </td><td>Slovenia     </td><td>90           </td><td>3            </td><td>GK           </td></tr>
	<tr><td>M. ter Stegen</td><td>Germany      </td><td>89           </td><td>3            </td><td>GK           </td></tr>
	<tr><td>T. Courtois  </td><td>Belgium      </td><td>89           </td><td>1            </td><td>GK           </td></tr>
	<tr><td>M. Neuer     </td><td>Germany      </td><td>89           </td><td>0            </td><td>GK           </td></tr>
	<tr><td>H. Lloris    </td><td>France       </td><td>88           </td><td>0            </td><td>GK           </td></tr>
</tbody>
</table>




<table>
<thead><tr><th scope=col>Name</th><th scope=col>Nationality</th><th scope=col>Overall</th><th scope=col>Score</th><th scope=col>Position</th></tr></thead>
<tbody>
	<tr><td>L. Messi         </td><td>Argentina        </td><td>94               </td><td>0                </td><td>RF               </td></tr>
	<tr><td>Cristiano Ronaldo</td><td>Portugal         </td><td>94               </td><td>0                </td><td>ST               </td></tr>
	<tr><td>Neymar Jr        </td><td>Brazil           </td><td>92               </td><td>1                </td><td>LW               </td></tr>
	<tr><td>E. Hazard        </td><td>Belgium          </td><td>91               </td><td>0                </td><td>LF               </td></tr>
	<tr><td>L. Suárez        </td><td>Uruguay          </td><td>91               </td><td>0                </td><td>RS               </td></tr>
	<tr><td>R. Lewandowski   </td><td>Poland           </td><td>90               </td><td>0                </td><td>ST               </td></tr>
	<tr><td>P. Dybala        </td><td>Argentina        </td><td>89               </td><td>5                </td><td>LF               </td></tr>
	<tr><td>H. Kane          </td><td>England          </td><td>89               </td><td>2                </td><td>ST               </td></tr>
	<tr><td>E. Cavani        </td><td>Uruguay          </td><td>89               </td><td>0                </td><td>LS               </td></tr>
	<tr><td>S. Agüero        </td><td>Argentina        </td><td>89               </td><td>0                </td><td>ST               </td></tr>
</tbody>
</table>




<table>
<thead><tr><th scope=col>Name</th><th scope=col>Nationality</th><th scope=col>Overall</th><th scope=col>Score</th><th scope=col>Position</th></tr></thead>
<tbody>
	<tr><td>K. De Bruyne   </td><td>Belgium        </td><td>91             </td><td>1              </td><td>RCM            </td></tr>
	<tr><td>L. Modrić      </td><td>Croatia        </td><td>91             </td><td>0              </td><td>RCM            </td></tr>
	<tr><td>T. Kroos       </td><td>Germany        </td><td>90             </td><td>0              </td><td>LCM            </td></tr>
	<tr><td>David Silva    </td><td>Spain          </td><td>90             </td><td>0              </td><td>LCM            </td></tr>
	<tr><td>N. Kanté       </td><td>France         </td><td>89             </td><td>1              </td><td>LDM            </td></tr>
	<tr><td>A. Griezmann   </td><td>France         </td><td>89             </td><td>1              </td><td>CAM            </td></tr>
	<tr><td>Sergio Busquets</td><td>Spain          </td><td>89             </td><td>0              </td><td>CDM            </td></tr>
	<tr><td>K. Mbappé      </td><td>France         </td><td>88             </td><td>7              </td><td>RM             </td></tr>
	<tr><td>M. Salah       </td><td>Egypt          </td><td>88             </td><td>1              </td><td>RM             </td></tr>
	<tr><td>Casemiro       </td><td>Brazil         </td><td>88             </td><td>2              </td><td>CDM            </td></tr>
</tbody>
</table>




<table>
<thead><tr><th scope=col>Name</th><th scope=col>Nationality</th><th scope=col>Overall</th><th scope=col>Score</th><th scope=col>Position</th></tr></thead>
<tbody>
	<tr><td>Sergio Ramos </td><td>Spain        </td><td>91           </td><td>0            </td><td>RCB          </td></tr>
	<tr><td>D. Godín     </td><td>Uruguay      </td><td>90           </td><td>0            </td><td>CB           </td></tr>
	<tr><td>G. Chiellini </td><td>Italy        </td><td>89           </td><td>0            </td><td>LCB          </td></tr>
	<tr><td>M. Hummels   </td><td>Germany      </td><td>88           </td><td>0            </td><td>LCB          </td></tr>
	<tr><td>Marcelo      </td><td>Brazil       </td><td>88           </td><td>0            </td><td>LB           </td></tr>
	<tr><td>Thiago Silva </td><td>Brazil       </td><td>88           </td><td>0            </td><td>RCB          </td></tr>
	<tr><td>S. Umtiti    </td><td>France       </td><td>87           </td><td>5            </td><td>CB           </td></tr>
	<tr><td>K. Koulibaly </td><td>Senegal      </td><td>87           </td><td>3            </td><td>LCB          </td></tr>
	<tr><td>Jordi Alba   </td><td>Spain        </td><td>87           </td><td>0            </td><td>LB           </td></tr>
	<tr><td>J. Vertonghen</td><td>Belgium      </td><td>87           </td><td>0            </td><td>LCB          </td></tr>
</tbody>
</table>




```R
squa433 <- data.frame(Name=c("De Gea","L. Messi","Cristiano Ronaldo","Neymar Jr",
                             "K. De Bruyne","T. Kroos","A. Griezmann","S. Umtiti","G. Chiellini","D. Godín","Sergio Ramos"),
                      Natioanlity=c("Spain","Argentina","Portugal","Brazil",
                                    "Belgium","Germany","France","France","Italy","Uruguay","Spain"),
                      Overall=c(91,94,94,92,91,90,89,87,89,90,91),
                      Position=c("GK","RF","ST","LW","RCM","LCM","CAM","CB","LCB","CB","RCB"))
squa433
mean(squa433$Overall)
```


<table>
<thead><tr><th scope=col>Name</th><th scope=col>Natioanlity</th><th scope=col>Overall</th><th scope=col>Position</th></tr></thead>
<tbody>
	<tr><td>De Gea           </td><td>Spain            </td><td>91               </td><td>GK               </td></tr>
	<tr><td>L. Messi         </td><td>Argentina        </td><td>94               </td><td>RF               </td></tr>
	<tr><td>Cristiano Ronaldo</td><td>Portugal         </td><td>94               </td><td>ST               </td></tr>
	<tr><td>Neymar Jr        </td><td>Brazil           </td><td>92               </td><td>LW               </td></tr>
	<tr><td>K. De Bruyne     </td><td>Belgium          </td><td>91               </td><td>RCM              </td></tr>
	<tr><td>T. Kroos         </td><td>Germany          </td><td>90               </td><td>LCM              </td></tr>
	<tr><td>A. Griezmann     </td><td>France           </td><td>89               </td><td>CAM              </td></tr>
	<tr><td>S. Umtiti        </td><td>France           </td><td>87               </td><td>CB               </td></tr>
	<tr><td>G. Chiellini     </td><td>Italy            </td><td>89               </td><td>LCB              </td></tr>
	<tr><td>D. Godín         </td><td>Uruguay          </td><td>90               </td><td>CB               </td></tr>
	<tr><td>Sergio Ramos     </td><td>Spain            </td><td>91               </td><td>RCB              </td></tr>
</tbody>
</table>




90.7272727272727


## Explanation: The best squared's average of overall score is 90. This is the dream team.

# ===================Champion===========================


```R
Nationality_team <- FIFA %>% filter(Overall > 80) %>% group_by(Nationality) %>% summarize("Average_team_Score" = sum(Overall))

head(Nationality_team[order(Nationality_team$Average_team_Score, decreasing = T), ], 10)
```


<table>
<thead><tr><th scope=col>Nationality</th><th scope=col>Average_team_Score</th></tr></thead>
<tbody>
	<tr><td>Spain    </td><td>5174     </td></tr>
	<tr><td>Brazil   </td><td>4272     </td></tr>
	<tr><td>France   </td><td>3260     </td></tr>
	<tr><td>Germany  </td><td>2931     </td></tr>
	<tr><td>Italy    </td><td>2495     </td></tr>
	<tr><td>Argentina</td><td>1681     </td></tr>
	<tr><td>Portugal </td><td>1663     </td></tr>
	<tr><td>Belgium  </td><td>1283     </td></tr>
	<tr><td>England  </td><td>1243     </td></tr>
	<tr><td>Croatia  </td><td> 920     </td></tr>
</tbody>
</table>



## Explanation: I droped the player whose score is lower than 80, then seperate into different Nationality group to get the rank of average of score of countries. Then, we can focus to analysis with this contries

# 1. Spain


```R
Nationality_team_Brazil <- FIFA %>% filter(Overall > 82 &  Nationality =="Brazil" ) %>% group_by(Position) %>% summarize("Average_Score" = mean(Overall))
Nationality_team_Brazil
mean(Nationality_team_Brazil$Average_Score)
```


<table>
<thead><tr><th scope=col>Position</th><th scope=col>Average_Score</th></tr></thead>
<tbody>
	<tr><td>CAM     </td><td>84.00000</td></tr>
	<tr><td>CB      </td><td>85.00000</td></tr>
	<tr><td>CDM     </td><td>86.00000</td></tr>
	<tr><td>GK      </td><td>84.66667</td></tr>
	<tr><td>LB      </td><td>85.75000</td></tr>
	<tr><td>LCB     </td><td>83.00000</td></tr>
	<tr><td>LCM     </td><td>83.00000</td></tr>
	<tr><td>LDM     </td><td>84.00000</td></tr>
	<tr><td>LM      </td><td>84.50000</td></tr>
	<tr><td>LW      </td><td>90.00000</td></tr>
	<tr><td>RCB     </td><td>85.50000</td></tr>
	<tr><td>RCM     </td><td>83.00000</td></tr>
	<tr><td>RM      </td><td>83.00000</td></tr>
	<tr><td>RW      </td><td>83.50000</td></tr>
	<tr><td>ST      </td><td>83.33333</td></tr>
</tbody>
</table>




84.55


# 2. France


```R
Nationality_team_France <- FIFA %>% filter(Overall > 82 &  Nationality =="France" ) %>% group_by(Position) %>% summarize("Average_Score" = mean(Overall))
Nationality_team_France
mean(Nationality_team_France$Average_Score)
```


<table>
<thead><tr><th scope=col>Position</th><th scope=col>Average_Score</th></tr></thead>
<tbody>
	<tr><td>CAM </td><td>86.0</td></tr>
	<tr><td>CB  </td><td>87.0</td></tr>
	<tr><td>CM  </td><td>83.0</td></tr>
	<tr><td>GK  </td><td>85.0</td></tr>
	<tr><td>LCB </td><td>83.5</td></tr>
	<tr><td>LDM </td><td>89.0</td></tr>
	<tr><td>LM  </td><td>83.5</td></tr>
	<tr><td>LW  </td><td>84.0</td></tr>
	<tr><td>RCB </td><td>86.0</td></tr>
	<tr><td>RDM </td><td>87.0</td></tr>
	<tr><td>RM  </td><td>86.0</td></tr>
	<tr><td>RW  </td><td>83.0</td></tr>
	<tr><td>ST  </td><td>85.0</td></tr>
</tbody>
</table>




85.2307692307692


# 3. Spain


```R
Nationality_team_Spain <- FIFA %>% filter(Overall > 82 &  Nationality =="Spain" ) %>% group_by(Position) %>% summarize("Average_Score" = mean(Overall))
Nationality_team_Spain
mean(Nationality_team_Spain$Average_Score)
```


<table>
<thead><tr><th scope=col>Position</th><th scope=col>Average_Score</th></tr></thead>
<tbody>
	<tr><td>CB      </td><td>83.00000</td></tr>
	<tr><td>CDM     </td><td>86.00000</td></tr>
	<tr><td>CM      </td><td>84.50000</td></tr>
	<tr><td>GK      </td><td>84.80000</td></tr>
	<tr><td>LB      </td><td>85.00000</td></tr>
	<tr><td>LCM     </td><td>90.00000</td></tr>
	<tr><td>LF      </td><td>86.00000</td></tr>
	<tr><td>LM      </td><td>85.00000</td></tr>
	<tr><td>LS      </td><td>84.00000</td></tr>
	<tr><td>LW      </td><td>88.00000</td></tr>
	<tr><td>RB      </td><td>84.33333</td></tr>
	<tr><td>RCB     </td><td>87.33333</td></tr>
	<tr><td>RCM     </td><td>84.33333</td></tr>
	<tr><td>RDM     </td><td>84.00000</td></tr>
	<tr><td>RM      </td><td>83.50000</td></tr>
	<tr><td>RW      </td><td>83.66667</td></tr>
	<tr><td>ST      </td><td>83.50000</td></tr>
</tbody>
</table>




85.1156862745098


# 4.Germany


```R
Nationality_team_Germany <- FIFA %>% filter(Overall > 82 &  Nationality =="Germany" ) %>% group_by(Position) %>% summarize("Average_Score" = mean(Overall))
Nationality_team_Germany
mean(Nationality_team_Germany$Average_Score)
```


<table>
<thead><tr><th scope=col>Position</th><th scope=col>Average_Score</th></tr></thead>
<tbody>
	<tr><td>CAM     </td><td>86.00000</td></tr>
	<tr><td>CB      </td><td>83.50000</td></tr>
	<tr><td>CM      </td><td>83.33333</td></tr>
	<tr><td>GK      </td><td>85.16667</td></tr>
	<tr><td>LCB     </td><td>88.00000</td></tr>
	<tr><td>LCM     </td><td>90.00000</td></tr>
	<tr><td>LM      </td><td>86.00000</td></tr>
	<tr><td>LW      </td><td>86.00000</td></tr>
	<tr><td>RB      </td><td>83.00000</td></tr>
	<tr><td>RCB     </td><td>85.00000</td></tr>
	<tr><td>RCM     </td><td>85.00000</td></tr>
	<tr><td>RW      </td><td>83.00000</td></tr>
	<tr><td>ST      </td><td>83.00000</td></tr>
</tbody>
</table>




85.1538461538462


# 5. Belgum


```R
Nationality_team_Belgium <- FIFA %>% filter(Overall > 82 &  Nationality =="Belgium" ) %>% group_by(Position) %>% summarize("Average_Score" = mean(Overall))
Nationality_team_Belgium
mean(Nationality_team_Belgium$Average_Score)
```


<table>
<thead><tr><th scope=col>Position</th><th scope=col>Average_Score</th></tr></thead>
<tbody>
	<tr><td>CAM</td><td>85 </td></tr>
	<tr><td>CB </td><td>85 </td></tr>
	<tr><td>CM </td><td>83 </td></tr>
	<tr><td>GK </td><td>89 </td></tr>
	<tr><td>LCB</td><td>87 </td></tr>
	<tr><td>LCM</td><td>84 </td></tr>
	<tr><td>LF </td><td>91 </td></tr>
	<tr><td>LM </td><td>83 </td></tr>
	<tr><td>RCB</td><td>86 </td></tr>
	<tr><td>RCM</td><td>91 </td></tr>
	<tr><td>RF </td><td>87 </td></tr>
	<tr><td>ST </td><td>87 </td></tr>
</tbody>
</table>




86.5


# 6.Argentina


```R
Nationality_team_Argentina <- FIFA %>% filter(Overall > 82 &  Nationality =="Argentina" ) %>% group_by(Position) %>% summarize("Average_Score" = mean(Overall))
Nationality_team_Argentina
mean(Nationality_team_Argentina$Average_Score)
```


<table>
<thead><tr><th scope=col>Position</th><th scope=col>Average_Score</th></tr></thead>
<tbody>
	<tr><td>CB </td><td>85 </td></tr>
	<tr><td>CDM</td><td>84 </td></tr>
	<tr><td>LF </td><td>89 </td></tr>
	<tr><td>LS </td><td>86 </td></tr>
	<tr><td>RF </td><td>94 </td></tr>
	<tr><td>RM </td><td>84 </td></tr>
	<tr><td>ST </td><td>88 </td></tr>
</tbody>
</table>




87.1428571428571


# 7. England


```R
Nationality_team_England <- FIFA %>% filter(Overall > 82 &  Nationality =="England" ) %>% group_by(Position) %>% summarize("Average_Score" = mean(Overall))
Nationality_team_England
mean(Nationality_team_England$Average_Score)

```


<table>
<thead><tr><th scope=col>Position</th><th scope=col>Average_Score</th></tr></thead>
<tbody>
	<tr><td>GK </td><td>83 </td></tr>
	<tr><td>LCM</td><td>84 </td></tr>
	<tr><td>RB </td><td>84 </td></tr>
	<tr><td>RCB</td><td>83 </td></tr>
	<tr><td>RW </td><td>86 </td></tr>
	<tr><td>ST </td><td>89 </td></tr>
</tbody>
</table>




84.8333333333333


# 8.Portugal 


```R
Nationality_team_Portugal <- FIFA %>% filter(Overall > 82 &  Nationality =="Portugal" ) %>% group_by(Position) %>% summarize("Average_Score" = mean(Overall))
Nationality_team_Portugal
mean(Nationality_team_Portugal$Average_Score)


```


<table>
<thead><tr><th scope=col>Position</th><th scope=col>Average_Score</th></tr></thead>
<tbody>
	<tr><td>CDM </td><td>83.5</td></tr>
	<tr><td>GK  </td><td>83.5</td></tr>
	<tr><td>LCM </td><td>83.5</td></tr>
	<tr><td>RCB </td><td>85.0</td></tr>
	<tr><td>RM  </td><td>84.0</td></tr>
	<tr><td>RW  </td><td>86.0</td></tr>
	<tr><td>ST  </td><td>94.0</td></tr>
</tbody>
</table>




85.6428571428571


# 9.Italy 


```R
Nationality_team_Italy <- FIFA %>% filter(Overall > 82 &  Nationality =="Italy" ) %>% group_by(Position) %>% summarize("Average_Score" = mean(Overall))
Nationality_team_Italy
mean(Nationality_team_Italy$Average_Score)
```


<table>
<thead><tr><th scope=col>Position</th><th scope=col>Average_Score</th></tr></thead>
<tbody>
	<tr><td>CB  </td><td>83.5</td></tr>
	<tr><td>CM  </td><td>84.0</td></tr>
	<tr><td>GK  </td><td>86.0</td></tr>
	<tr><td>LCB </td><td>89.0</td></tr>
	<tr><td>LCM </td><td>86.0</td></tr>
	<tr><td>LS  </td><td>83.0</td></tr>
	<tr><td>LW  </td><td>88.0</td></tr>
	<tr><td>RCB </td><td>86.0</td></tr>
	<tr><td>RDM </td><td>83.0</td></tr>
	<tr><td>ST  </td><td>87.0</td></tr>
</tbody>
</table>




85.55


## Rank


```R
Champions_predict <- data.frame(
                      Natioanlity=c("England","Argentina","Portugal","Brazil",
                                    "Belgium","Germany","France","Spain","Italy"),
                      Overall=c(84.833,87.142,85.642,84.55,86.5,85.153,85.23,85.115,85.55))
                    

head(Champions_predict[order(Champions_predict$Overall, decreasing = T), ], 8)


```


<table>
<thead><tr><th></th><th scope=col>Natioanlity</th><th scope=col>Overall</th></tr></thead>
<tbody>
	<tr><th scope=row>2</th><td>Argentina</td><td>87.142   </td></tr>
	<tr><th scope=row>5</th><td>Belgium  </td><td>86.500   </td></tr>
	<tr><th scope=row>3</th><td>Portugal </td><td>85.642   </td></tr>
	<tr><th scope=row>9</th><td>Italy    </td><td>85.550   </td></tr>
	<tr><th scope=row>7</th><td>France   </td><td>85.230   </td></tr>
	<tr><th scope=row>6</th><td>Germany  </td><td>85.153   </td></tr>
	<tr><th scope=row>8</th><td>Spain    </td><td>85.115   </td></tr>
	<tr><th scope=row>1</th><td>England  </td><td>84.833   </td></tr>
</tbody>
</table>



## Explanation: it appears that the Argentina will be the next champion.

# 5.)===============Simple Linear Regression====================

### a. Potential capability


```R
ScoreLM <- lm(Score ~ Age, data = FIFA) 
summary(ScoreLM)

new <- data.frame(Age = 22) 
result <- predict(ScoreLM, newdata = new) 


ggplot(FIFA, aes(x = Age , y = Score )) +geom_point(shape = 10, size = 3) + 
geom_point(x = new$Age, y = result, size = 10, shape = 17, color = "red")+ 
geom_smooth(method = lm)+
geom_point(shape = 7, size = 1) + labs(x = "Age", y = "Score") 
```


    
    Call:
    lm(formula = Score ~ Age, data = FIFA)
    
    Residuals:
        Min      1Q  Median      3Q     Max 
    -9.2057 -2.1869 -0.1994  1.7985 14.8507 
    
    Coefficients:
                 Estimate Std. Error t value Pr(>|t|)    
    (Intercept) 30.243294   0.110668   273.3   <2e-16 ***
    Age         -1.002089   0.004331  -231.4   <2e-16 ***
    ---
    Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
    
    Residual standard error: 2.729 on 18205 degrees of freedom
    Multiple R-squared:  0.7462,	Adjusted R-squared:  0.7462 
    F-statistic: 5.353e+04 on 1 and 18205 DF,  p-value: < 2.2e-16






![png](output_70_2.png)


## Explanation:
### After we analyze the Score(overall - potential) which means the player who has higher score is higher potential, we found younger player has higher chance to inspire their potential. On the other hand, the older player has stable performance in matches.

### b. CAM position and Curve Correlation 


```R
correlation<- select(FIFA, CAM,
                     Crossing,Finishing,HeadingAccuracy,ShortPassing,
                        Volleys,Dribbling,Curve,FKAccuracy,
                        LongPassing,BallControl,Acceleration,SprintSpeed,Agility,Reactions)

pairs.panels(correlation[,-5], 
             method = "pearson", # correlation method
             hist.col = "#00AFBB",
             density = TRUE,  # show density plots
             ellipses = TRUE # show correlation ellipses
)
```


![png](output_73_0.png)



```R
model2 <- lm(CAM ~ Curve, data = FIFA) 
summary(model2)

new2 <- data.frame(Curve = 70) 
result2 <- predict(model2, newdata = new2) 


ggplot(FIFA, aes(x = Curve , y = CAM )) +geom_point(shape = 10, size = 2) + 
geom_point(x = new2$Curve, y = result2, size = 10, shape = 17, color = "red")+ 
geom_smooth(method = lm)+
geom_point(shape = 7, size = 1) + labs(x = "Curve", y = "CAM") 
```


    
    Call:
    lm(formula = CAM ~ Curve, data = FIFA)
    
    Residuals:
         Min       1Q   Median       3Q      Max 
    -30.4398  -3.6287   0.0726   3.7593  23.5206 
    
    Coefficients:
                 Estimate Std. Error t value Pr(>|t|)    
    (Intercept) 32.718114   0.163979   199.5   <2e-16 ***
    Curve        0.512443   0.003068   167.0   <2e-16 ***
    ---
    Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
    
    Residual standard error: 5.9 on 16120 degrees of freedom
      (2085 observations deleted due to missingness)
    Multiple R-squared:  0.6338,	Adjusted R-squared:  0.6337 
    F-statistic: 2.79e+04 on 1 and 16120 DF,  p-value: < 2.2e-16



    Warning message:
    “Removed 2085 rows containing non-finite values (stat_smooth).”Warning message:
    “Removed 2085 rows containing missing values (geom_point).”Warning message:
    “Removed 2085 rows containing missing values (geom_point).”




![png](output_74_3.png)


## Explanation:
### CAM position Score has correlation with Curve Score. The R squared value is up to 0.6. So, it appears that the player in CAM (central attack midfield) position needs has a good curve skill.

### c. ST position and Dribbling Correlation


```R
correlation<- select(FIFA, ST,
                     Crossing,Finishing,HeadingAccuracy,ShortPassing,
                        Volleys,Dribbling,Curve,FKAccuracy,
                        LongPassing,BallControl,Acceleration,SprintSpeed,Agility,Reactions)

pairs.panels(correlation[,-5], 
             method = "pearson", # correlation method
             hist.col = "#00AFBB",
             density = TRUE,  # show density plots
             ellipses = TRUE # show correlation ellipses
)
```


![png](output_77_0.png)



```R
model3 <- lm(ST ~Dribbling , data = FIFA) 
summary(model3)

new3 <- data.frame(Dribbling = 80) 
result3 <- predict(model3, newdata = new3) 


ggplot(FIFA, aes(x = Dribbling , y = ST )) +geom_point(shape = 10, size = 2) + 
geom_point(x = new3$Dribbling, y = result3, size = 10, shape = 17, color = "red")+ 
geom_smooth(method = lm)+
geom_point(shape = 7, size = 1) + labs(x = "Dribbling", y = "ST") 
```


    
    Call:
    lm(formula = ST ~ Dribbling, data = FIFA)
    
    Residuals:
         Min       1Q   Median       3Q      Max 
    -20.8756  -3.3132  -0.0005   3.3119  21.2287 
    
    Coefficients:
                 Estimate Std. Error t value Pr(>|t|)    
    (Intercept) 21.208556   0.197896   107.2   <2e-16 ***
    Dribbling    0.604173   0.003199   188.9   <2e-16 ***
    ---
    Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
    
    Residual standard error: 5.081 on 16120 degrees of freedom
      (2085 observations deleted due to missingness)
    Multiple R-squared:  0.6888,	Adjusted R-squared:  0.6888 
    F-statistic: 3.568e+04 on 1 and 16120 DF,  p-value: < 2.2e-16



    Warning message:
    “Removed 2085 rows containing non-finite values (stat_smooth).”Warning message:
    “Removed 2085 rows containing missing values (geom_point).”Warning message:
    “Removed 2085 rows containing missing values (geom_point).”




![png](output_78_3.png)


## Explanation:
### Strike position Score has correlation with Dribbling Score. The R squared value is up to 0.6. So, it appears that the player in Strike position needs has a good Dribbling skill.

### d. Strike position and Finishing score Correlation


```R
model4 <- lm(ST ~ Finishing, data = FIFA) 
summary(model4)

new4 <- data.frame(Finishing = 50) 
result4 <- predict(model4, newdata = new4) 


ggplot(FIFA, aes(x = Finishing , y = ST )) +geom_point(shape = 10, size = 2) + 
geom_point(x = new4$Finishing, y = result4, size = 10, shape = 17, color = "red")+ 
geom_smooth(method = lm)+
geom_point(shape = 7, size = 1) + labs(x = "Finishing", y = "ST") 
```


    
    Call:
    lm(formula = ST ~ Finishing, data = FIFA)
    
    Residuals:
         Min       1Q   Median       3Q      Max 
    -13.9179  -2.8295  -0.0357   2.7074  18.4422 
    
    Coefficients:
                 Estimate Std. Error t value Pr(>|t|)    
    (Intercept) 33.300934   0.106502   312.7   <2e-16 ***
    Finishing    0.492633   0.002033   242.3   <2e-16 ***
    ---
    Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
    
    Residual standard error: 4.227 on 16120 degrees of freedom
      (2085 observations deleted due to missingness)
    Multiple R-squared:  0.7846,	Adjusted R-squared:  0.7846 
    F-statistic: 5.872e+04 on 1 and 16120 DF,  p-value: < 2.2e-16



    Warning message:
    “Removed 2085 rows containing non-finite values (stat_smooth).”Warning message:
    “Removed 2085 rows containing missing values (geom_point).”Warning message:
    “Removed 2085 rows containing missing values (geom_point).”




![png](output_81_3.png)


## Explanation:
### Strike position Score has correlation with Finishing Score. The R squared value is up to 0.6. So, it appears that the player in Strike position needs has a good Finishing skill.

### e. Strike position and BallControl Score Correlation


```R
model5 <- lm(ST ~ BallControl, data = FIFA) 
summary(model5)

new5 <- data.frame(BallControl = 50) 
result5 <- predict(model5, newdata = new5) 


ggplot(FIFA, aes(x = BallControl , y = ST )) +geom_point(shape = 10, size = 2) + 
geom_point(x = new5$BallControl, y = result5, size = 10, shape = 17, color = "red")+ 
geom_smooth(method = lm)+
geom_point(shape = 7, size = 1) + labs(x = "BallControl", y = "ST") 
```


    
    Call:
    lm(formula = ST ~ BallControl, data = FIFA)
    
    Residuals:
         Min       1Q   Median       3Q      Max 
    -18.9822  -3.2698   0.0292   3.3508  24.6034 
    
    Coefficients:
                Estimate Std. Error t value Pr(>|t|)    
    (Intercept) 9.144035   0.243994   37.48   <2e-16 ***
    BallControl 0.770103   0.003813  201.97   <2e-16 ***
    ---
    Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
    
    Residual standard error: 4.848 on 16120 degrees of freedom
      (2085 observations deleted due to missingness)
    Multiple R-squared:  0.7167,	Adjusted R-squared:  0.7167 
    F-statistic: 4.079e+04 on 1 and 16120 DF,  p-value: < 2.2e-16



    Warning message:
    “Removed 2085 rows containing non-finite values (stat_smooth).”Warning message:
    “Removed 2085 rows containing missing values (geom_point).”Warning message:
    “Removed 2085 rows containing missing values (geom_point).”




![png](output_84_3.png)


## Explanation:
### Strike position Score has correlation with BallControl Score. The R squared value is up to 0.6. So, it appears that the player in Strike position needs has a good BallControl skill.

# 6.)============Multiple Linear Regression====================

### a. Stirke


```R
StikeMuLiRe <- lm(ST ~  BallControl +Finishing+Dribbling, data = FIFA) 
summary(StikeMuLiRe)
```


    
    Call:
    lm(formula = ST ~ BallControl + Finishing + Dribbling, data = FIFA)
    
    Residuals:
         Min       1Q   Median       3Q      Max 
    -10.3119  -1.7757   0.0704   1.7948  11.1555 
    
    Coefficients:
                 Estimate Std. Error t value Pr(>|t|)    
    (Intercept) 14.818836   0.136828  108.30   <2e-16 ***
    BallControl  0.380569   0.003999   95.17   <2e-16 ***
    Finishing    0.311816   0.001815  171.83   <2e-16 ***
    Dribbling    0.056569   0.003453   16.38   <2e-16 ***
    ---
    Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
    
    Residual standard error: 2.651 on 16118 degrees of freedom
      (2085 observations deleted due to missingness)
    Multiple R-squared:  0.9153,	Adjusted R-squared:  0.9153 
    F-statistic: 5.807e+04 on 3 and 16118 DF,  p-value: < 2.2e-16



## Explanation:
### it appears that the ballcontrol, finishing, and dribbling can affect the Strike position

### b. Goal Keeper


```R
GKPlayer <- lm(GKPositioning ~  GKDiving +GKHandling+GKKicking+GKReflexes, data = FIFA) 
summary(GKPlayer)
```


    
    Call:
    lm(formula = GKPositioning ~ GKDiving + GKHandling + GKKicking + 
        GKReflexes, data = FIFA)
    
    Residuals:
         Min       1Q   Median       3Q      Max 
    -21.0124  -2.5030   0.0032   2.5034  20.0922 
    
    Coefficients:
                Estimate Std. Error t value Pr(>|t|)    
    (Intercept) 0.274385   0.035414   7.748 9.84e-15 ***
    GKDiving    0.249895   0.007261  34.418  < 2e-16 ***
    GKHandling  0.276458   0.007274  38.007  < 2e-16 ***
    GKKicking   0.198950   0.006854  29.029  < 2e-16 ***
    GKReflexes  0.251408   0.007198  34.927  < 2e-16 ***
    ---
    Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
    
    Residual standard error: 3.378 on 18154 degrees of freedom
      (48 observations deleted due to missingness)
    Multiple R-squared:  0.9607,	Adjusted R-squared:  0.9607 
    F-statistic: 1.109e+05 on 4 and 18154 DF,  p-value: < 2.2e-16



## Explanation:
### it appears that the GKDiving, GKReflexes, GKHandling, and GKKicking are inportant skill for goal keepers. 

## c. Central Attack Midfield


```R
CAMplayer <- lm(CAM ~  BallControl +Finishing+Curve, data = FIFA) 
summary(CAMplayer)
```


    
    Call:
    lm(formula = CAM ~ BallControl + Finishing + Curve, data = FIFA)
    
    Residuals:
         Min       1Q   Median       3Q      Max 
    -14.1063  -1.5700   0.1379   1.7090  13.4916 
    
    Coefficients:
                Estimate Std. Error t value Pr(>|t|)    
    (Intercept) 6.980396   0.139960   49.87   <2e-16 ***
    BallControl 0.600602   0.003258  184.33   <2e-16 ***
    Finishing   0.157291   0.001747   90.05   <2e-16 ***
    Curve       0.121293   0.002084   58.20   <2e-16 ***
    ---
    Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
    
    Residual standard error: 2.662 on 16118 degrees of freedom
      (2085 observations deleted due to missingness)
    Multiple R-squared:  0.9254,	Adjusted R-squared:  0.9254 
    F-statistic: 6.669e+04 on 3 and 16118 DF,  p-value: < 2.2e-16





## Explanation:
### it appears that the BallControl, Finishing, and Curve are inportant skill for central attack midfield. 

## d. Central Back


```R
correlation<- select(FIFA, CB,
                     Vision,Penalties,Composure,Stamina,Strength,Marking,Interceptions,Aggression,StandingTackle,
                    SlidingTackle)

pairs.panels(correlation[,-5], 
             method = "pearson", # correlation method
             hist.col = "#00AFBB",
             density = TRUE,  # show density plots
             ellipses = TRUE # show correlation ellipses
)
```


![png](output_98_0.png)



```R
CBplayer <- lm(CB ~  Interceptions+Marking+StandingTackle+SlidingTackle, data = FIFA) 
summary(CBplayer)
```


    
    Call:
    lm(formula = CB ~ Interceptions + Marking + StandingTackle + 
        SlidingTackle, data = FIFA)
    
    Residuals:
         Min       1Q   Median       3Q      Max 
    -10.8627  -1.9557  -0.0014   1.8917  12.5823 
    
    Coefficients:
                    Estimate Std. Error t value Pr(>|t|)    
    (Intercept)    23.055172   0.074268 310.432   <2e-16 ***
    Interceptions   0.242164   0.003441  70.386   <2e-16 ***
    Marking         0.178942   0.002882  62.080   <2e-16 ***
    StandingTackle  0.212328   0.005431  39.095   <2e-16 ***
    SlidingTackle   0.002866   0.004836   0.593    0.553    
    ---
    Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
    
    Residual standard error: 2.975 on 16117 degrees of freedom
      (2085 observations deleted due to missingness)
    Multiple R-squared:  0.9354,	Adjusted R-squared:  0.9354 
    F-statistic: 5.833e+04 on 4 and 16117 DF,  p-value: < 2.2e-16



# 7.)==================Summary====================

### The range of player age is from 20 to 26. It appears that the number of players who is 21 years old is over 1400. And next, the nationality rank appears that up to 1600 players come from England. And then is Germany and Spain. Next, up to 76 percent players preferred foot is right. Only 23 percent players use left foot. In the valuable players rank, you can see the most valuable player is Neymar and then is Messi and the third is bruyne.
### Then, I did some adaption. Because in this dataset, there is two columns: Overall score and potential score. After, the potential score column minus overall score column, I got the potential growth score. This score can allow us to understand easily the players possible developments in the future. The table shows that the players who have higher score are young. Only 17 or 16. 
### in linear regression, I analyze the correlation between age and potential growth. The R squared value up to 0.7. So, the formula appears that there is a correlation between this two. More young more potential growth score. Next, there is some explanation of position. This is list of abbreviations. In soccer, we have different formations, this is a common one in soccer game. Then, we can separate the ground into three different part. Forward, Midfield, and back or defensive. In each part we have several position like in defensive we have goal keeper, sweeper, left central back. In forward, strike, right strike. We have 32 different positions, I choose one position in each part to predict. 
### First one I chose strike. In this plot, I use ball control, finishing, dribbling to make simple linear regression, it appears that strike position has correlation with this three factors. So, we can say the player in this position need to good at ball control, finishing, and dribbling. Moreover, we also use this three to make multiple linear regression. I found the this formula R squared is up to 0.91. It’s a good formula to predict strike. So, in the same way, I found four formula with high R-squared for different positions. Central attack midfield players need good ball control, finishing, and curve. Central back need good interception, marking, standing tackle, and sliding tackle. The last formula for goal keeper has up to 0.96 R squared. Goal keeper need to have good diving, handing, kicking, and reflexes skill. Those formula allows us to predict which player is suitable on which position. 
### The last part, the best squared. Like we said before, we analyze the common formation 4-3-3. We need three in midfield, three for forward, and four for defensives. I separated the positions into different group. And choose the players the formation need from each rank. This is our dream team. And the next, the most important part is which national team will be the next champion. I analyze the average of team score. Then, I pick up top nine nationality to analyze, I calculated average score in different position. Here is the final average score. According to that score, the champion will be Argentina. 

# 8.)=================Report====================

![]("data:image/png;base64,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")

![]("data:image/png;base64,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")

### The best squared 
1. GK   - De Gea                From Spain
2. RF    - L. Messi              From Argentina
3. ST    -Cristiano Ronaldo  From  Portugal
4. LW   -Neymar Jr             From Brazil
5. RCM -K. De Bruyne         From Belgium
6. LCM -T. Kroos                From Germany
7. CAM -A. Griezmann         From France
8. CB    -S. Umtiti               From France
9. LCB  -G. Chiellini            From Italy
10. CB    -D. Godín               From Uruguay
11. RCB  -Sergio Ramos       From Spain

### The next champion will be
![](data:image/png;base64,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)
