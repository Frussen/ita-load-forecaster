# ItaLoadForecaster – PoC Previsioni Carico Elettrico Italiano

## Obiettivo
Previsione oraria del carico elettrico italiano (2020 hold-out) usando dati open ENTSO-E/OPSD.

- Baseline: Prophet (seasonality + regressors prezzo/solar)
- Avanzato: LSTM (sequenze 168h, non-linearità, picchi)

## Risultati chiave (test 2020)
- **Prophet baseline**: MAE 3077.20 MW, MAPE 9.89%
- **LSTM avanzato**: MAE 323.27 MW, MAPE 1.11%  
  → Miglioramento: -89.5% MAE / -88.8% MAPE vs Prophet
- **Vs forecast ufficiale ENTSO-E**: MAPE 1.11% vs 2.39% (LSTM migliore su hindcast)

## ROI differenziale stimato
- Miglioramento vs ufficiale ENTSO-E: ~423 MW meno errore per ora
- Energia risparmiata (test): ~3.645M MWh
- Assunzioni conservative: 30% errore causa costo reale, 150 €/MWh imbalance
- **Risparmi annui stimati**: **€ 166–170 milioni** per player medio

## Struttura PoC (10 giorni)
1. Setup + ingestion dati
2. EDA + cleaning
3. Feature engineering (lags, rolling, ciclici, interazioni)
4. Baseline Prophet
5. Eval Prophet
6. LSTM avanzato
7. Eval LSTM + ROI
8. MLOps (MLflow logging, salvataggio)
9. Dashboard Streamlit (live: [link Space])
10. Conclusione e pitch

## Come usare
- **Dashboard interattiva**: [https://huggingface.co/spaces/Frussen/ItaLoadForecaster](https://huggingface.co/spaces/Frussen/ItaLoadForecaster) 
  - Seleziona LSTM/Prophet → grafico forecast vs actual, metriche, ROI
- **Codice completo**: notebook principale (ItaLoadForecaster.ipynb)
- **Modello salvato** + scalers: in MLflow runs (o file .h5/.pkl)

## Prossimi step
- Pilot con dati reali clienti (Enel-like)
- Tuning LSTM (hyperparametri, window size, feature extra)
- Integrazione forecast solare/prezzo day-ahead in produzione
- Deployment su infrastruttura enterprise (inference API)

PoC validato: salto da MAPE 9.89% (Prophet) a 1.11% (LSTM) – valore economico concreto e scalabile.
