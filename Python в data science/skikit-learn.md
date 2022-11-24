### Функции  
- **tree.DecisionTreeClassifier** - класс дерева решений. Можно выбрать критерий, например criterion='entropy'  
- **clf.fit(X, y)** - обучить дерево по предикторам X и результату y. clf - объект класса DecisionTreeClassifier. Стоит ограничить max_depth  
- **clf.predict(X)** - предсказать на основе обученной модели  
- **clf.score(X, y)** - проверить модель на тестовых данных. Возвращает точность [0; 1]  
- **tree.plot_tree(clf)** - отобразить картинку, наглядно показывающую дерево решений и энтропию каждого сплита  
- **model_selection.train_test_split** - разделить данные на две группы. Например, на обучающую и тестовую  
Ex: ```X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.33, random_state=42)```   
- **model_selection.cross_val_score** - инструмент для [[Деревья решений#Кроссвалидация|кроссвалидации]]  
Ex: `cross_val_score(clf, X_train, y_train, cv=5`   
Вывод это массив из пяти *точностей* валидации для каждых 4-х сплитов