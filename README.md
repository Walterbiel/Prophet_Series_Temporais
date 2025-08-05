# Estudos com Prophet para Séries Temporais

Este repositório tem como objetivo documentar estudos e testes realizados com o modelo **Prophet**, desenvolvido pela Meta (Facebook), para previsão de séries temporais. O foco principal é explorar o seu funcionamento, aplicações práticas e boas práticas de modelagem.

## 🔧 Tecnologias utilizadas

- Python 3.10+
- [Prophet](https://facebook.github.io/prophet/)
- Pandas
- Matplotlib / Plotly
- Jupyter Notebook (opcional)

## 📂 Estrutura do Projeto

```
Prophet_Series_Temporais/
├── dados/                 # Conjunto de dados de exemplo (csv, excel, etc.)
├── notebooks/             # Cadernos Jupyter com exemplos práticos
├── src/                   # Scripts Python reutilizáveis
├── resultados/            # Gráficos e previsões salvas
├── README.md
└── requirements.txt
```

## 📈 Objetivos

- [x] Entender a estrutura esperada pelo Prophet (`ds` e `y`)
- [x] Ajustar modelos com dados reais (ex: vendas, cotação, clima)
- [x] Adicionar feriados e sazonalidades personalizadas
- [x] Avaliar desempenho com métricas como MAPE, RMSE, etc.
- [x] Comparar com outros modelos (ARIMA, LSTM, etc.)

## 📘 Exemplos de uso

### Pré-processamento básico

```python
import pandas as pd
from prophet import Prophet

df = pd.read_csv("dados/vendas.csv")
df.rename(columns={"data": "ds", "vendas": "y"}, inplace=True)

model = Prophet()
model.fit(df)

future = model.make_future_dataframe(periods=30)
forecast = model.predict(future)

model.plot(forecast);
```

## 📊 Resultados esperados

- Compreensão clara das capacidades do Prophet
- Aplicações práticas para negócios reais
- Base para estudos mais avançados com séries temporais

## 📝 Referências

- [Documentação Oficial do Prophet](https://facebook.github.io/prophet/docs/quick_start.html)
- [Artigo original do Prophet (2017)](https://peerj.com/preprints/3190/)
- Cursos de Data Science e Machine Learning em português

---

## ✅ Como executar localmente

```bash
git clone https://github.com/Walterbiel/Prophet_Series_Temporais.git
cd Prophet_Series_Temporais
pip install -r requirements.txt
```

---

Feito com 💙 para estudos de Data Science em português.  
Mais conteúdos em [gptonline.ai](https://gptonline.ai/)
