# Metryki

## 1. Metryki klasyfikacji

1\. **Confusion Matrix (Macierz Pomyłek)** - pozwala na sprawdzenie jakie błędy w testach popełnił model.

|             | Przewidziana klasa 0 | Przewidziana klasa 1 |
| :---------: | :------------------: | :------------------: |
| **Klasa 0** | TN (True Negative)   | FP (False Positive)  |
| **Klasa 1** | FN (False Negative)  | TP (True Positive)   |

Interpretacja dla macierzy 2x2:
- TN - ilość przypadków, gdy model przewidział klasę 0 i prawidłową klasą też jest klasa 0.
- TP - ilość przypadków, gdy model przewidział klasę 1 i prawidłową klasą też jest klasa 1.
- FP - ilość przypadków, gdy model  przewidział klasę 1, a prawidłową klasą jest klasa 0.
- FN - ilość przypadków, gdy model przewidział klasę 0, a prawidłową klasą jest klasa 1.

```python
from sklearn.metrics import confusion_matrix

# y_test - rzeczywiste numery klas; y_pred - przewidziane przez model numery klas
print(confusion_matrix(y_test, y_pred))
```

2\. **Accuracy (Dokładność)** - procent wszystkich poprawnych predykcji. Jeśli klasy są zbalansowane to metryka ta działa dość dobrze, ale w przeciwnym przypadku może ona być dość niedokładną miarą. Jeśli wszystkie przypadki model przewidzi jako jedną klasę, a przykładowo proporcje dwóch klas rozkładają się 9:1 to mimo, że model osiągnął 90% to model jest bezużyteczny, ponieważ każdy przypadek interpretuje jako jedną klasę. W takich wypadkach lepiej jest przetestować wyniki modelu za pomocą innych dokładniejszych metryk.

Wzór dla 2 klas:

$$
Accuracy = \frac{TP + TN}{TP + TN + FP + FN}
$$

Dla większej ilości klas **Accuracy** liczona jest poprzez dodanie wszystkich poprawnych przypadków i podzielenie tego przez sumę wszystkich przypadków.

```python
from sklearn.metrics import accuracy_score

# y_test - rzeczywiste numery klas; y_pred - przewidziane przez model numery klas
print(accuracy_score(y_test, y_pred))
```

3\. **Recall (Czułość)** - spośród wszystkich znalezionych przypadków należących do danej klasy, ile model znalazł naprawdę. Metryka zatem uwzględnia pozytywne przewidziane przypadki oraz przypadki, gdzie dana klasa nie została rozpoznana/wykryta.

$$
Recall = \frac{TP}{TP + FN}
$$

Dla większej ilości klas jest więcej wartości FN i leżą one poziomo (wiersz).

```python
from sklearn.metrics import recall_score

# y_test - rzeczywiste numery klas; y_pred - przewidziane przez model numery klas
print(recall_score(y_test, y_pred))
```

4\. **Precision (Precyzja)** - spośród wszystkich przypadków, które model wskazał jako daną klasę, ile tak naprawdę z tych przypadków należy do tej klasy. Metryka zatem uwzględnia pozytywne przewidziane przypadki oraz przypadki, gdzie inna klasa została przewidziana jako klasa badana, a powinna być inna, czyli model błędnie zinterpretował, np. gdy TP = klasa 1, FP = klasa 1 (chociaż faktyczna klasa to 0 - lub inna jeśli klas jest więcej).

$$
Precision = \frac{TP}{TP + FP}
$$

Dla większej ilości klas jest więcej wartości FP i leżą one pionowo (kolumna).

```python
from sklearn.metrics import precision_score

# y_test - rzeczywiste numery klas; y_pred - przewidziane przez model numery klas
print(precision_score(y_test, y_pred))
```

5\. **F1-score** - średnia harmoniczna precision i recall. Metryka karze za skrajności, czyli uwzględnia błędy w niewykrywaniu klasy jak (recall) i jej nadmiernym wykrywaniu (przypadkach, gdy inna klasa jest interpretowana jako dana klasa, precision).

$$
F1 = 2 \cdot \frac{Precision \cdot Recall}{Precision + Recall}
$$

```python
from sklearn.metrics import f1_score

# y_test - rzeczywiste numery klas; y_pred - przewidziane przez model numery klas
print(f1_score(y_test, y_pred))
```

## 2. Metryki regresji

1\. **MAE (Mean Absolute Error)** - średnia wartość pomiędzy prawdziwą a przewidzianą wartością w jednostkach szukanej wartości, np. złotych, kilogramach, metrach itp.

$$
MAE = \frac{1}{n} \sum_{i=1}^{n} |y_i - \hat{y_i}|,
$$
gdzie:
- $y_i$ - prawdziwa wartość dla i-tej próbki
- $\hat{y_i}$ - przewidywana wartość dla i-tej próbki
- n - liczba próbek

```python
from sklearn.metrics import mean_absolute_error

# y_test - rzeczywiste wartości; y_pred - przewidziane wartości przez model
print(mean_absolute_error(y_test, y_pred))
```

2\. **MSE (Mean Squared Error)** - średnia kwadratów błędów.

$$
MSE = \frac{1}{n} \sum_{i=1}^{n} (y_i - \hat{y_i})^2,
$$

gdzie:
- $y_i$ - prawdziwa wartość dla i-tej próbki
- $\hat{y_i}$ - przewidywana wartość dla i-tej próbki
- n - liczba próbek

```python
from sklearn.metrics import mean_squared_error

# y_test - rzeczywiste wartości; y_pred - przewidziane wartości przez model
print(mean_squared_error(y_test, y_pred))
```

3\. **RMSE (Root Mean Squared Error)** - określa katastrofalne błędy, czyli duże różnice pomiędzy faktyczną wartością, a tą przewidzianą przez model. 

$$
RMSE = \sqrt{MSE} = \sqrt{\frac{1}{n} \sum_{i=1}^{n} (y_i - \hat{y_i})^2},
$$

gdzie:
- $y_i$ - prawdziwa wartość dla i-tej próbki
- $\hat{y_i}$ - przewidywana wartość dla i-tej próbki
- n - liczba próbek

```python
import numpy as np
from sklearn.metrics import mean_squared_error

# y_test - rzeczywiste wartości; y_pred - przewidziane wartości przez model
print(np.sqrt(mean_squared_error(y_test, y_pred)))
```

4\. **R<sup>2</sup> (Współczynnik determinacji)** - porównuje przewidziane wartości modelu ze średnią wszystkich prawdziwych wartości.

$$
R^2 = 1 - \frac{\sum_{i=1}^{n} (y_i - \hat{y_i})^2}{\sum_{i=1}^{n} (y_i - \bar{y_i})^2},
$$

gdzie:
- $y_i$ - prawdziwa wartość dla i-tej próbki
- $\hat{y_i}$ - przewidywana wartość dla i-tej próbki
- $\bar{y_i}$ - średnia wszystkich prawdziwych wartości ($\bar{y_i} = \frac{1}{n} \sum_{i=1}^{n} y_i$)
- n - liczba próbek

```python
from sklearn.metrics import r2_score

# y_test - rzeczywiste wartości; y_pred - przewidziane wartości przez model
print(r2_score(y_test, y_pred))
```
