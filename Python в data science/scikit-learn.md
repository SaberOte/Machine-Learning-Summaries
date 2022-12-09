### Функции  
- **tree.DecisionTreeClassifier** - класс дерева решений. Можно выбрать критерий, например criterion='entropy', ограничить max_depth и min_samples_split/min_samples_leaf  
- **clf.fit(X, y)** - обучить дерево по предикторам X и результату y. clf - объект класса DecisionTreeClassifier  
- **clf.predict(X)** - предсказать на основе обученной модели  
- **clf.score(X, y)** - проверить модель на тестовых данных. Возвращает точность [0; 1]  
- **tree.plot_tree(clf)** - отобразить картинку, наглядно показывающую дерево решений и энтропию каждого сплита  
- **model_selection.train_test_split** - разделить данные на две группы. Например, на обучающую и тестовую  
Ex: ```X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.33, random_state=42)```   
Существует много аналогов, для "правильного" разделения. Используется также для кроссвалидации. Подробнее в [документации](https://scikit-learn.org/stable/modules/cross_validation.html)  
![Pasted image 20221126120137.png](https://github.com/PolkaDott/Data-Science-Summaries/blob/main/Python%20в%20data%20science/attachments/Pasted%20image%2020221126120137.png?raw=true)  
- **model_selection.cross_val_score** - инструмент для [[Деревья решений#Кроссвалидация|кроссвалидации]]. cv принимает число либо объект с настройками кроссвалидации  
Ex: `cross_val_score(clf, X_train, y_train, cv=5)`   
Вывод это массив из пяти *точностей* валидации для каждых 4-х сплитов  
- **metrics.precision_score(y_true, y_pred)** - расчитать метрику Precision. Аналогичная есть для Recall и F score (recall_score, f1_score)  
- **model_selection.GridSearchCV** - автоматически перебрать переданные параметры и выбрать те, у которых лучшая предсказательная способность  
Ex: ```clf = tree.DecisionTreeClassifier()  
parameters = {'criterion' : ['gini', 'entropy'], 'max_depth' : range(1,30)}  
grid_search_cv_clf = GridSearchCV(clf, parameters, cv=5) # cv-crossvalidation  
grid_search_cv_clf.fit(X, y)  
best_clf = grid_search_cv_clf.best_estimator_  
best_params = grid_search_cv_clf.best_params_ # {'criterion': 'entropy', 'max_depth': 5}```  
- **model_selection.RandomizedSearchCV** - *GridSearchCV* может быть медленным из-за перебора. Рандомный аналог делает значительно быстрее, пробегаясь по рандомным параметрам  
- **clf.predict_proba(X)** - получить не просто результаты предсказаний, а набор из пар вероятностей отнесения к классам  
-   
### Предобработка  
- Чтобы нормализовать данные (сделать среднее = 0, а стандартное отклонение = 1), используется класс `preprocessing.StandardScaler`.   
Пример использования:```  
scaler = StandardScaler()  
scaler.fit(X_train)  
X_train_scaled = scaler.transform(X_train)```  
- Чтобы не создавать лишних переменных (я так понял), можно использовать *Pipeline*, в который можно пихнуть всякие стандартизаторы, и последним аргументом классификатор/регрессор и прочее