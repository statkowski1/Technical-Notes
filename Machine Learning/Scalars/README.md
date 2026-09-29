# Skalary

**Skaler (Scaler)** - transformer, który przekształca wartości cech numerycznych, aby doprowadzić je do wspólnej skali. Jeśli cechy w modelu mają wyższą skalę, np. cena mieszkania: 10 000 zł i wymiar mieszkania to: 100 m<sup>2</sup> to występuję zbyt duża różnica i cena może zacząć dominować nad wymiarem mieszkania. Niektóre modele wymagają przeskalowania takich cech, aby trening się udał.

1\. **StandardScaler** - przekształca każdą cechę tak, aby średnia wynosiła 0, a odchylenie standardowe 1.

$$
x_{scaled} = \frac{x - \mu}{\sigma},
$$

gdzie:
- $\sigma$ - Odchylenie standardowe:

$$
\sigma = \sqrt{\frac{1}{n} \sum_{i=1}^{n} (x_i - \mu)^2}
$$

- $\mu$ - średnia

```python
from sklearn.preprocessing import StandardScaler

scaler = StandardScaler()

X_train[columns] = scaler.fit_transform(X_train[columns])
X_test[columns] = scaler.transform(X_test[columns])
```

2\. **MinMaxScaler** - przekształca każdą cechę tak, aby wartości były w przedziale [0, 1].

$$
x_{scaled} = \frac{x - x_{min}}{x_{max} - x_{min}}
$$

```python
from sklearn.preprocessing import MinMaxScaler

scaler = MinMaxScaler()

X_train[columns] = scaler.fit_transform(X_train[columns])
X_test[columns] = scaler.transform(X_test[columns])
```
Używając StandardScaler() lub MinMaxScaler():
1. **fit_transform()** - stosuje się na zbiorze treningowym i oblicza on dla **skalarów** na podstawie danych ze zbioru treningowego odpowiednie informacje, które potem wykorzysta na przekształcenie zbioru testowego:
- **StandardScaler()**: $\mu$ (średnia), $\sigma$ (odchylenie standardowe);
- **MinMaxScaler()**: $x_{max}$, $x_{min}$.
2. **transform()** - stosuje się na zbiorze testowym i wykorzystuje wartości obliczone wcześniej na podstawie danych ze zbioru treningowego.