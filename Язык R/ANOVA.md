## Уравнения  
DV ~ IV # One-way  
  
DV ~ IV1 + IV2 # Two-way  
  
DV ~ IV1:IV2  # Two-way interaction  
  
DV ~ IV1 + IV2 + IV1:IV2 # Main effects + interaction  
  
DV ~ IV1 * IV2  # The same: Main effects + interaction  
  
DV ~ IV1 + IV2 + IV3 + IV1:IV2  
  
DV ~ (IV1 + IV2 + IV3)^2 # main effects and all possible interactions up to level 2  
  
DV ~ IV1 + Error(subject/IV1) # repeated measures  
  
## Функции  
- #### **aov** - провести дисперсионный анализ  
- #### **summary** - показать краткую информацию об анализе  
Ex: ```fit <- aov(price ~ origin, data=mydata)  
summary(fit)```  
-|   Df |Sum Sq  | Mean Sq  | F value | Pr(>F)  
-|-|-|-|-|-  
origin   |    1  | 94107  | 94107 |   6.65 | 0.0189 |   
Residuals   | 18 | 254729 |  14152 |  |   |             
- #### **model.tables** - вывести метрические значения по группам  
Ex: ```fit1 <- aov(price ~ origin + store, data=mydata)  
summary(fit1)  
model.tables(fit1,"means")```  
Out:  
#### Tables of means  
**Grand mean** *192.7745*  
**origin**  
import | russia   
-|-  
261.37 | 124.18   
**store**  
 minimarket | supermarket   
 -|-  
     204.98  |    180.57   
- #### **TukeyHSD** - взять выборки из aov и сравнить ихвсе попарно🤡  
### Взаимодействие факторов  
![[Pasted image 20220916132304.png|400]]  
Когда случаются ситуации, как на картинке выше, что выборка по одной группе может давать различимость иную от выборки по другой группе, можно использовать дисперсионный анализ с учётом взаимодействия:  
`fit3 <- aov(price ~ origin + store + origin:store, data=mydata)`  
`summary(fit3)`  
 -|Df | Sum Sq  |Mean Sq |F value | Pr(>F)  
 -|-|-|-|-|-  
origin  |      1  |94107  | 94107|   7.968 |0.0123  
store       |  1  | 2981  |  2981 |  0.252 | 0.6222  
origin:store   | 1 | 62777 |  62777  | 5.315  | 0.0349  
Residuals |   16 | 188971 |  11811 | |                
  
### Анализ с учётом повторных измерений  
Если одному субъекту принадлежит несколько строк в дата фрейме, то может быть проблема, если втупую сравнивать один показатель, не учитывая фактор испытуемого.   
Примеры, как учесть испытуемого:  
1.   
`fit1b <- aov(well_being ~ therapy + Error(subject/therapy), data = mydata2)`  
`summary(fit1b)`  
2. Учитываются два критерия  
`fit2b <- aov(well_being ~ therapy*price + Error(subject/(therapy*price)), data = mydata2)`  
`summary(fit2b)`  
3. Учитываются 3 критерия, но *пол* не учитывается в ошибке  
`fit3b <- aov(well_being ~ therapy*price*sex + Error(subject/(therapy*price)), data = mydata2)`  
`summary(fit3b)`  
Вывод третьего примера:  
**Error: subject**  
-|      Df | Sum Sq | Mean Sq | F value | Pr(>F)  
-|-|-|-|-|-  
sex     |   1  | 45.8  | 45.82   | 0.169  |0.709  
Residuals | 3   | 814.2 | 271.40      | |          
**Error: subject:therapy**  
-|            Df| Sum Sq |Mean Sq |F value| Pr(>F)  
-|-|-|-|-|-  
therapy    |  2 | 426.8  | 213.4  | 0.476  |0.643  
therapy:sex | 2  | 70.1 |   35.1 |  0.078| 0.926  
Residuals   | 6 |2690.2  | 448.4     | |          
**Error: subject:price**  
-|Df| Sum Sq |Mean Sq| F value| Pr(>F)  
-|-|-|-|-|-  
price    |  1 |1674.8 | 1674.8   |6.704 |0.0811  
price:sex | 1  |255.3  | 255.3|   1.022| 0.3865  
Residuals  |3 | 749.5 |  249.8                 
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1  
**Error: subject:therapy:price**  
-|Df |Sum Sq |Mean Sq| F value |Pr(>F)  
-|-|-|-|-|-  
therapy:price     | 2   |57.2    |28.6   |0.083|  0.921  
therapy:price:sex | 2  |212.2 |  106.1  | 0.310  |0.745  
Residuals      |    6 | 2055.7  | 342.6 | |