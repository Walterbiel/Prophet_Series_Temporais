# 📈 Documentação Completa - Previsões com Facebook Prophet

Este guia aborda, passo a passo, o uso do Facebook Prophet para modelar séries temporais, com foco em sazonalidade, feriados, outliers, validação cruzada, crescimento e muito mais.

> 🔗 Mais recursos em: [https://gptonline.ai/](https://gptonline.ai/)

---

## 🔧 Instalação

```bash
pip install prophet matplotlib pandas scipy
```

---

## 📈 Carregamento e Preparação de Dados

```python
df = pd.read_csv("co2-ppm-daily_csv.csv")
df['date'] = pd.to_datetime(df['date'])
df.columns = ['ds', 'y']
```

---

## 🔮 Modelagem Básica

```python
model = Prophet()
model.fit(df)

future = model.make_future_dataframe(periods=365 * 10)
forecast = model.predict(future)

fig = model.plot(forecast)
plt.show()

fig2 = model.plot_components(forecast)
plt.show()
```

---

## 🗓️ Frequências Diferentes

### Dados Mensais

```python
df = pd.read_csv("AirPassengers.csv")
df['Month'] = pd.to_datetime(df['Month'])
df.columns = ['ds', 'y']
model = Prophet(seasonality_mode="multiplicative")
future = model.make_future_dataframe(periods=12*5, freq='MS')
```

### Dados Horários

```python
df = pd.read_csv("divvy_hourly.csv")
df['date'] = pd.to_datetime(df['date'])
df.columns = ['ds', 'y']
future = model.make_future_dataframe(periods=365*24, freq='h')
```

### Dados com Gaps Regulares

```python
df = df[(df['ds'].dt.hour >= 8) & (df['ds'].dt.hour < 18)]
future = model.make_future_dataframe(periods=365*24, freq='h')
future = future[(future['ds'].dt.hour >= 8) & (future['ds'].dt.hour < 18)]
```

---

## ⚙️ Modos de Sazonalidade

- `additive`: variação constante.
- `multiplicative`: variação proporcional.

```python
model = Prophet(seasonality_mode='multiplicative')
```

---

## 🌀 Controlar Complexidade: Fourier Order

```python
model = Prophet(yearly_seasonality=4)
model.add_seasonality(name='11-year cycle', period=11*365.25, fourier_order=5)
```

---

## 🧐 Sazonalidade Condicional

```python
df['weekend'] = df['ds'].dt.dayofweek >= 5
model.add_seasonality(name='daily_weekend', period=1, fourier_order=3, condition_name='weekend')
```

---

## ⚖️ Regularização

```python
model = Prophet(seasonality_prior_scale=0.01, holidays_prior_scale=10)
```

---

## 🇺🇸 Feriados

### Por País

```python
model.add_country_holidays(country_name='US')
```

### Por Estado

```python
make_holidays_df(year_list, country='US', state='IL')
```

### Personalizados

```python
black_friday = pd.DataFrame({'holiday': 'Black Friday', 'ds': pd.to_datetime([...])})
```

---

## 📉 Modos de Crescimento

- `linear`
- `logistic` (requer `cap`)
- `flat`

```python
model = Prophet(growth='logistic')
df['cap'] = 500
```

---

## 🔄 Change Points

```python
model = Prophet(n_changepoints=25, changepoint_prior_scale=0.05)
```

---

## ➕ Regressões

### Categóricas

```python
model.add_regressor('weather')
```

### Contínuas

```python
model.add_regressor('temp')
```

---

## ⚠️ Outliers

- Winsorization
- Z-score
- Média Móvel
- Intervalo de Confiança
- Eventos especiais

---

## 📊 Validação Cruzada

```python
from prophet.diagnostics import cross_validation, performance_metrics
cv = cross_validation(model, initial='730 days', period='30 days', horizon='90 days')
performance_metrics(cv)
```

---

## 🚀 Otimização

```python
param_grid = {
  'changepoint_prior_scale': [0.1, 0.01],
  'seasonality_prior_scale': [10.0, 1.0],
  'seasonality_mode': ['additive','multiplicative']
}
```

---

## ✅ Conclusão

Prophet é uma ferramenta poderosa para previsão de séries temporais com muitos recursos customizáveis.

---


