# ATR in Ticks for TradingView

Stop distances in price points can be hard to translate into an instrument's
minimum price increments.
This Pine Script v6 indicator plots smoothed true range in ticks or price points.
Choose a smoothing method, multiplier, and optional calculation timeframe to
inspect volatility in a separate pane.

![ATR plot on five-minute gold futures](assets/images/atr-in-ticks-indicator.jpeg)

The image shows gold futures on a five-minute chart with a 0.5 multiplier.
Tick counts depend on each symbol's minimum price increment.
They do **not** make volatility, risk, or position sizes directly comparable
across markets.
The plot supplies a volatility measure, not a stop-loss or position-sizing recommendation.

- [Add the indicator and explore examples](docs/usage.md).
- [Check settings, calculation, and timeframe limitations](docs/reference.md).
- [Look up the domain terms](GLOSSARY.md).
- [Read the Pine source](atr-ticks-multiplier.pine) and [license](LICENSE.md).

Contributions are welcome through issues for bugs and feature requests.
