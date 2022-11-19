# Модульна контрольна робота 2

Для виконання модульної контрольної роботи треба: 

1. завантажити вибірку даних;
2. провести масштабування ознак вибірки;
3. провести стратифіковану крос-валідацію з 10 блоками та вивести середній показник правильності моделі;
4. за допомогою класу `GridSearchCV` знайти оптимальні гіперпараметри для моделі за допомогою гратчастого пошуку та 5-блочної стратифікованої крос-валідації;
5. вивести в консоль оптимальні параметри та середню правильність на тестовій вибірці, отримані за допомогою `GridSearchCV`;
6. візуалізувати результати гратчастого пошуку з крос-валідацією за допомогою теплової карти;
7. навчити модель з використанням знайдених оптимальних гіперпараметрів;
8. Отримати матрицю помилок для навченої моделі;
9. Отримати звіт стосовно моделі за допомогою функції `classification_report` та вивести його в консоль;
10. Отримати зображення кривої влучності-повноти, зробити висновки щодо співвідношення влучності та повноти;
12. Отримати зображення ROC-кривої, зробити висновки щодо якості моделі із зовнішнього зображення кривої;
13. Отримати та вивести значення AUC для отриманної ROC-кривої.
14. Використовуючи значення AUC, за допомогою класу `GridSearchCV` знайти оптимальні гіперпараметри для моделі за допомогою гратчастого пошуку та 5-блочної стратифікованої крос-валідації.

Вибірки та моделі машинного навчання відрізняються для кожного варіанту МКР. Варіант обирається згідно до порядкового номеру студенту у списку групи.

МКР виконується у вигляді python notebook, який ви можете створити в Google Colab. Після виконання МКР, збережіть файл на диску та завантажте його у наступній google-формі - https://forms.gle/PE8Dn373fbuY3fRD9

## Вибірка даних 

Для кожного варіанту вказано `id` вибірки, яку треба завантажити. Вибірки даних для різних варіантів:
- Варіант 1 - 334
- Варіант 2 - 1464
- Варіант 3 - 333
- Варіант 4 - 1494
- Варіант 5 - 1510
- Варіант 6 - 1489
- Варіант 7 - 37
- Варіант 8 - 1487
- Варіант 9 - 1479
- Варіант 10 - 1063
- Варіант 11 - 334
- Варіант 12 - 1464
- Варіант 13 - 333
- Варіант 14 - 1494
- Варіант 15 - 1510
- Варіант 16 - 1489
- Варіант 17 - 37
- Варіант 18 - 1487 
- Варіант 19 - 1479
- Варіант 20 - 1063

### Перелік моделей:

1. Випадковий ліс (Random Forest). Параметри:
  
```python
param_grid = {'n_estimators': [100, 200, 500, 1000, 2000],
              'max_depth': [3, 5, 7, 9, 11]}
```

При отриманні значення AUC використовуйте наступні параметри функції

```python
roc_auc_score(y_test, model.predict_proba(X_test)[:, 1])
```

2. GradientBoosting. Параметри:

```python
param_grid = {'max_depth': [2, 4, 6, 8, 10],
              'learning_rate': [0.01, 0.1, 1, 10, 100]}
```

При отриманні значення AUC використовуйте наступні параметри функції

```python
roc_auc_score(y_test, model.predict_proba(X_test)[:, 1])
```

3. SVM RBF kernel. Параметри:

```python
param_grid = {'C': [0.001, 0.1, 10, 1000, 100000],
              'gamma': [0.001, 0.1, 10, 1000, 100000]}
```

При отриманні значення AUC використовуйте наступні параметри функції

```python
roc_auc_score(y_test, model.decision_function(X_test))
```

4. Logistic regression. Параметри:

```python
param_grid = {'C': [0.001, 0.01, 0.1, 1, 10, 100, 1000, 10000, 100000],
              'solver': ['newton-cg', 'lbfgs', 'liblinear', 'sag', 'saga']}
```

При отриманні значення AUC використовуйте наступні параметри функції

```python
roc_auc_score(y_test, model.decision_function(X_test))
```

Моделі для різних варіантів:

- Варіант 1 - 1
- Варіант 2 - 2
- Варіант 3 - 3
- Варіант 4 - 4
- Варіант 5 - 1
- Варіант 6 - 2
- Варіант 7 - 3
- Варіант 8 - 4
- Варіант 9 - 1
- Варіант 10 - 2
- Варіант 11 - 3
- Варіант 12 - 4
- Варіант 13 - 1
- Варіант 14 - 2
- Варіант 15 - 3
- Варіант 16 - 4
- Варіант 17 - 1
- Варіант 18 - 2
- Варіант 19 - 3
- Варіант 20 - 4

```python
# Код для завантаження та масштабування вибірки

import pandas as pd
import numpy as np
from sklearn.datasets import fetch_openml
from sklearn.preprocessing import StandardScaler

data = fetch_openml(data_id = 9999) # використовуйте id вибірки згідно вашого варіанту
X = data.data
y = data.target

sc = StandardScaler()
sc.fit(X)

X = sc.transform(X)
y = y.values

```
