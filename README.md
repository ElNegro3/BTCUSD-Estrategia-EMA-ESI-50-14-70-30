/@version=5
indicator("BTCUSD Estrategia EMA + RSI", overlay=true)

// Parámetros
emaLength = input.int(50, "EMA Periodo")
rsiLength = input.int(14, "RSI Periodo")
rsiOverbought = input.int(70, "RSI Sobrecompra")
rsiOversold = input.int(30, "RSI Sobreventa")

// Cálculos
ema = ta.ema(close, emaLength)
rsi = ta.rsi(close, rsiLength)

// Señales
longSignal = close > ema and rsi < rsiOversold
shortSignal = close < ema and rsi > rsiOverbought

// Gráficos
plot(ema, color=color.orange, title="EMA")
plotshape(longSignal, title="Compra", style=shape.labelup, color=color.green, text="BUY")
plotshape(shortSignal, title="Venta", style=shape.labeldown, color=color.red, text="SELL")

// Alertas
alertcondition(longSignal, title="Señal de Compra", message="BTCUSD: Señal de COMPRA detectada")
alertcondition(shortSignal, title="Señal de Venta", message="BTCUSD: Señal de VENTA detectada")
