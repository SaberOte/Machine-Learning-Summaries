#### [Cсылка](https://seaborn.pydata.org/examples/index.html) на документацию  
  
#### Полезные графики  
- **pairplot** - матрица с разными графиками для попарного сравнения всех ячеек  
Ex1: `sns.pairplot(df, vars=df.columns[:-1], diag_kind='kde')`  
![Pasted image 20221116155507.png|400](https://github.com/PolkaDott/Data-Science-Summaries/blob/main/Python%20в%20data%20science/attachments/Pasted%20image%2020221116155507.png?raw=true)  
Ex2: ```df = sns.load_dataset("penguins")  
g = sns.PairGrid(df, diag_sharey=False)  
g.map_upper(sns.scatterplot, s=20)  
g.map_lower(sns.kdeplot)  
g.map_diag(sns.kdeplot, lw=1)```  
![Pasted image 20221116155636.png|400](https://github.com/PolkaDott/Data-Science-Summaries/blob/main/Python%20в%20data%20science/attachments/Pasted%20image%2020221116155636.png?raw=true)  
- **subplots** - матрица с отдельными графиками  
Ex: ```g.map_diag(sns.kdeplot, lw=1)  
f, axes = plt.subplots(2, 2, figsize=(12, 7), sharex=True)  
sns.histplot( df["sepal length"] , color="skyblue", ax=axes[0, 0])  
sns.kdeplot( df["sepal width"] , color="olive", ax=axes[0, 1])  
sns.kdeplot( df, x='sepal width', y='sepal length' , color="gold", ax=axes[1, 0])  
sns.histplot( df["petal width"] , color="teal", ax=axes[1, 1])```  
![Pasted image 20221116161101.png|500](https://github.com/PolkaDott/Data-Science-Summaries/blob/main/Python%20в%20data%20science/attachments/Pasted%20image%2020221116161101.png?raw=true)