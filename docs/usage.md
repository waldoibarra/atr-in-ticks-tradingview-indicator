# Use ATR in Ticks

Add the indicator in TradingView's Pine Editor, then choose settings for your
chart. The examples illustrate readings, not trading recommendations.

## Add to a chart

1. Open TradingView and its Pine Editor.
2. Select **Create new**, then **Indicator**.
3. Copy the entire [`atr-ticks-multiplier.pine`](../atr-ticks-multiplier.pine)
   source into the editor.
4. Select **Save**, name the indicator, then select **Add to Chart**.

The indicator plots a red line in a separate pane.
See the [settings and calculation reference](reference.md) for exact defaults
and output units.

## Interpret a stop-distance example

Suppose the plot reads 50 ticks at a 1.0 multiplier on a five-minute chart.
These hypothetical distances multiply that displayed reading; they do not
determine a suitable stop.

```text
1.5x to 2.0x multiplier: 75 to 100 ticks
1.0x to 1.5x multiplier: 50 to  75 ticks
0.5x to 1.0x multiplier: 25 to  50 ticks
```

Set the indicator multiplier to 0.5 or 2.0 to see a scaled reading.
Position sizing also requires your instrument's tick value and your own risk
limits.

## Inspect a broader timeframe

Choose a 60-minute indicator timeframe on a five-minute chart to inspect
hourly ATR.
The **Wait for timeframe closes** switch selects a gap mode for
`request.security()`.
It does not guarantee closed higher-timeframe values or prevent repainting.
See [timeframe behavior](reference.md#timeframe-behavior) before using that
reading for decisions.

## Try smoothing and trading contexts

RMA is the default smoothing method for the 14-period reading.
EMA weights recent true ranges differently; SMA averages equally across its
window. WMA uses linearly weighted recent values.
These settings illustrate different contexts; none establishes an appropriate
risk level.

| Context | Example settings | Intended inspection |
| --- | --- | --- |
| Day trading | 14, RMA, 1.5, chart | Intraday volatility for stops |
| Swing trading | 14, RMA, 2.0, daily on four-hour | Daily context |
| Scalping | 7, EMA, 1.0, chart | Shorter, more responsive reading |
| Position trading | 20, RMA, 3.0, weekly | Longer-period distance planning |

The table lists periods, smoothing, multiplier, and timeframe in that order.
For chart-based entries, use the chart timeframe; choose a higher timeframe
for broader context.
Multipliers such as 0.5, 1, 1.5, 2, or 3 change the displayed reading.
Keep tick display on when your task calls for distances in minimum price
increments.
Choose RMA for the default method or EMA for stronger weighting of recent
values.
Do not treat **Wait for timeframe closes** as a repaint-prevention control.

## Troubleshoot readings

### Values differ from TradingView's built-in ATR

Tick display is on by default, while built-in ATR commonly displays price
units. Disable **Display in ticks (instead of points)** to compare units.
Compare the same symbol, timeframe, length, and RMA smoothing with a 1.0
multiplier.
Matching settings alone do not establish identical results across all chart
histories or data feeds.

### The plot has gaps

With a selected timeframe, **Wait for timeframe closes** selects
`barmerge.gaps_on`. That mode can leave chart bars without a mapped value.
Disable it to select `barmerge.gaps_off`, which fills gaps with available
mapped values.
The code does not independently confirm when a higher-timeframe bar closes.

### Tick counts differ across markets

A tick is the symbol's minimum price increment, not a common monetary or
volatility unit.
Check each market's tick size and tick value before comparing risk or sizing
positions.
