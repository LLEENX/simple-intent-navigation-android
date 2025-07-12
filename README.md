```python
# Siapkan data untuk Prophet
prophet_df = close_prices.reset_index()[['Date', 'Close']]
prophet_df.columns = ['ds', 'y']  # Prophet butuh kolom 'ds' untuk tanggal dan 'y' untuk nilai

# Buat model dan latih
prophet_model = Prophet(daily_seasonality=True)
prophet_model.fit(prophet_df)

# Buat dataframe tanggal untuk 10 hari ke depan
future_dates = prophet_model.make_future_dataframe(periods=10)

# Lakukan prediksi
forecast = prophet_model.predict(future_dates)

# Visualisasikan hasil forecast
fig1 = prophet_model.plot(forecast)
plt.title('Prediksi Harga Saham UNVR Menggunakan Prophet')
plt.xlabel('Tanggal')
plt.ylabel('Harga (IDR)')
plt.grid(True)
plt.show()
```
