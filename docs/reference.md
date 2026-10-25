# ATR in Ticks reference

The indicator calculates true range, smooths it, and plots a scaled value.
Its output uses ticks by default; turn off tick display to use price units.

![Indicator inputs showing defaults](../assets/images/indicator-settings.jpeg)

## Settings

| Input | Default | Behavior |
| --- | --- | --- |
| Length (Periods) | 14 | Smoothing length; minimum 1. |
| Smoothing | RMA | RMA, SMA, EMA, or WMA. |
| Multiplier | 1.0 | Scale output; minimum 0.1, step 0.1. |
| Display in ticks (instead of points) | On | Off uses price units. |
| Timeframe | Chart | Empty input uses chart bars. |
| Wait for timeframe closes | On | On uses gaps; off fills them. |

**Timeframe** and **Wait for timeframe closes** appear in the
**CALCULATION** input group.
The indicator is a Pine Script v6 plot in a separate pane.
Its `ATR Value` line uses red (`#b71c1c`).
The source attributes the script to `waldoibarra` and includes an MPL 2.0
notice. Read the [license](../LICENSE.md) for the full terms.

## Calculation

1. Calculate true range with `ta.tr(true)`.
2. Smooth that series using the selected moving average and length.
3. Use that value directly or request it on the selected timeframe.
4. For tick display, divide by `syminfo.mintick`, then apply
   `math.round_to_mintick()` to the quotient.
5. Multiply the rounded quotient and apply `math.ceil()` for the plotted
   tick value.

With tick display off, the plot multiplies the smoothed price-unit value
without that rounding or ceiling.
The source labels this internal value `atrInPoints`; its unit follows the
chart symbol's prices.
See the [glossary](../GLOSSARY.md) for true range, ATR, and tick terminology.

## Timeframe behavior

An empty **Timeframe** input calculates directly on chart bars.
A selected timeframe calls `request.security()` using the selected timeframe,
symbol, and session.
**Wait for timeframe closes** selects `barmerge.gaps_on` when enabled and
`barmerge.gaps_off` otherwise.
Gap settings control how requested values map to chart bars.
The source specifies neither a confirmed-bar offset nor a separate
repaint-prevention mechanism.
Do not infer guaranteed higher-timeframe closure or non-repainting behavior
from the switch's label.
TradingView runtime behavior, including live-bar updates and alignment,
remains unverified here.

## Comparison limits

The default length, RMA smoothing, and 1.0 multiplier support a like-for-like
comparison setup.
Turn off tick display when comparing price-unit readings with TradingView's
built-in ATR.
This repository has no TradingView runtime test proving exact parity.
Tick counts across symbols still reflect different minimum increments and
monetary tick values.
The output alone cannot establish equivalent volatility, risk, or position
size across markets.
