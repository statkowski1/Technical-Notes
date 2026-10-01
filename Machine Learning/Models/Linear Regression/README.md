# Regresja Liniowa

**Regresja Liniowa** - model uczenia maszynowego, który przewiduje wartość ciągłą (**model regresyjny**) na podstawie kombinacji liniowej (wyrażenie powstające poprzez pomnożenie danych obiektów, np. macierzy, a następnie ich dodanie do siebie) cech wejściowych.

Wzór modelu:

$$
\hat{y} = w_0 + w_1 x_1 + ... + w_n x_n,
$$

Gdzie:
- $\hat{y}$ - przewidywana wartość (y_pred)
- x_1, ..., x_n - cechy wejściowe (danej próbki, X_test)
- w_0 - obliczony wyraz wolny (bias)
- w_1, ..., w_n - obliczone wagi

**Normal Equation**

$$
w = (X^TX)^{-1} X^T y,
$$

Gdzie:
- X - połączona kolumna jedynek z macierzą cech (1 kolumna jedynek, X_train)
- y - wektor prawdziwych wartości (y_train)
- w - obliczone wagi modelu

```python
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_absolute_error, mean_squared_error, r2_score

model = LinearRegression()
model.fit(X_train, y_train)

y_pred = model.predict(X_test)

print('MAE (Średni Błąd Bezwzględny): ', mean_absolute_error(y_test, y_pred))
print('RMSE (Pierwiastek Błędu Średniokwadratowego): ', np.sqrt(mean_squared_error(y_test, y_pred)))
print('R^2 (Współczynnik Determinacji): ', r2_score(y_test, y_pred))
```
Funkcja **Regresji Liniowej** z biblioteki **sklearn** używa metody **Normal Equation** do obliczania wag.