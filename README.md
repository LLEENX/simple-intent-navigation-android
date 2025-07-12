```python
# Ambil harga terakhir aktual
last_actual_date = close_prices.index[-1]
last_actual_price = float(close_prices.iloc[-1]['Close'])  # pastikan float

# Ambil 10 prediksi terakhir Prophet
prophet_pred = forecast.set_index('ds')['yhat'].tail(10)

# Gabungkan prediksi Prophet dengan titik akhir aktual
prophet_combined_dates = [last_actual_date] + list(prophet_pred.index)
prophet_combined_values = [last_actual_price] + [float(val) for val in prophet_pred.values]

# Plot
plt.figure(figsize=(12,6))
plt.plot(close_prices[-100:], label='Aktual (100 Hari Terakhir)', color='blue')
plt.plot(prophet_combined_dates, prophet_combined_values, label='Prediksi Prophet', color='green', linestyle='--')
plt.title('Perbandingan Prediksi LSTM vs Prophet (10 Hari ke Depan)')
plt.xlabel('Tanggal')
plt.ylabel('Harga (IDR)')
plt.legend()
plt.grid(True)
plt.show()
```
