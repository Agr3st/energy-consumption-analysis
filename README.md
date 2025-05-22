# 📊 Energy Consumption Analysis and Forecasting in Spain (2015–2018)

Celem projektu jest analiza zużycia energii elektrycznej oraz zbudowanie modelu umożliwiającego krótkoterminową i długoterminową prognozę zapotrzebowania energetycznego w Hiszpanii na podstawie danych z lat 2015–2018. Projekt uwzględnia wpływ różnych czynników zewnętrznych, takich jak warunki pogodowe i cechy czasowe, a także przedstawia wyniki w formie wizualizacji umożliwiających interpretację trendów i zależności.

---

## 📂 Dane

Dane zostały pobrane z [Kaggle: Energy Consumption, Generation, Prices and Weather](https://www.kaggle.com/datasets/nicholasjhana/energy-consumption-generation-prices-and-weather)

Wykorzystane pliki:
- `energy_dataset.csv` – rzeczywiste zużycie energii
- `weather_features.csv` – dane pogodowe z 5 największych miast Hiszpanii (uśrednione)

---

## 📈 Etapy projektu

### 1. Przetwarzanie danych (`data_processing.ipynb`)
- Wczytanie danych zużycia i danych pogodowych
- Uśrednienie cech pogodowych dla całego kraju
- Scalenie zbiorów i interpolacja braków
- Formatowanie danych i zapis do `energy_and_weather_data.csv`

⚠️ Uwaga: dane pogodowe zostały uśrednione dla 5 największych miast, co nie odzwierciedla w pełni lokalnych warunków atmosferycznych w całym kraju. W rezultacie wpływ pogody na zużycie energii może być w modelu częściowo wygładzony lub niedoszacowany.

### 2. Eksploracja danych (`eda.ipynb`)
- Statystyki opisowe dla każdej cechy
- Wykresy:
  - Rozkład zużycia energii ogółem i wg lat
  - Średnie dobowe i miesięczne zużycie energii
  - Zużycie energii względem dnia tygodnia i godziny
  - Macierz korelacji cech
  - Zależność zużycia energii od temperatury i wilgotności

### 3. Modelowanie (`model.ipynb`)
- Inżynieria cech czasowych (`hour`, `dayofweek`, `month`) i rolling features
- Model regresji: `RandomForestRegressor` + GridSearchCV
- Podział na zbiór treningowy (2015–2017) i testowy (2018)
- Zapis modelu do `model/model.pkl`
- Ocena:
  - MAE: 1180.77  
  - RMSE: 1695.92  
  - MAPE: 4.09%

### 4. 📉 Predykcja (`prediction.ipynb`)
- Predykcja zużycia energii dla ostatnich **7 i 30 dni** 2018 roku
- Zapis wyników do `data/processed/pred_7_days.csv` i `pred_30_days.csv`
- Wizualizacja:
  - Porównanie danych rzeczywistych z predykcją (7-dniowa, 30-dniowa)
  - Porównanie danych rzeczywistych z predykcją (30-dniową) z podświetleniem okresów, gdzie **temperatura ma istotny wpływ** (wysoka korelacja z zużyciem energii)

---

## 🗂️ Struktura katalogów
```
.
├── data/
│   ├── raw/                           # Surowe dane z Kaggle
│   │   ├── energy_dataset.csv
│   │   └── weather_features.csv
│   └── processed/                     # Dane scalone i przetworzone
│       ├── energy_and_weather_data.csv
│       ├── energy_and_weather_data_for_model.csv
│       ├── pred_7_days.csv
│       └── pred_30_days.csv
│
├── model/
│   └── model.pkl                      # Zapisany model
│
├── notebooks/
│   ├── data_processing.ipynb          # Przetwarzanie danych
│   ├── eda.ipynb                      # Eksploracja danych
│   ├── model.ipynb                    # Trening i walidacja modelu
│   └── prediction.ipynb               # Predykcja i wizualizacje
│
├── plots/
│   ├── prediction_7_days.png
│   ├── prediction_30_days.png
│   ├── prediction_30_days_with_temperature.png
│   ├── prediction_7_30_days_with_temperature.png
│   └── ...                            # inne wykresy
│
└── README.md
```
