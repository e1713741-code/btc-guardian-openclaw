# BTC Guardian — Personal Risk Control Agent

Retail crypto traders all face the same problem: they make small profits but lose big. Every quant app out there talks about returns and strategies, but almost none focus on the one thing that actually keeps you alive — **dynamic, personal risk control**.

BTC Guardian is an autonomous AI agent that monitors your trading behavior and market conditions 24/7, matches them against 59 proven risk control strategies, and proactively protects your capital — before you make emotional decisions.

This agent:

• Connects to your quantitative trading platform (FMZ) via API to track your positions, trade frequency, and account equity in real time • Runs scheduled market scans every 5 minutes — checking BTC price action, volatility (ATR/VIX), funding rates, and on-chain indicators like MVRV Z-Score • When risk signals are detected, Agnes Claw reasons over 59 strategies across 13 categories (trend following, mean reversion, volatility breakout, oscillators, etc.) to find the best risk control response • Pushes actionable alerts to Telegram: "Your trade frequency is abnormally high today — emotional circuit breaker activated, positions locked for 4 hours" • If authorized, auto-executes protective actions via FMZ API: reduce position size, set dynamic stop-loss, or trigger black swan hedging

## Skills you Need

* `web_fetch` (built-in) — for pulling real-time market data
* `knowledge-base` skill — for storing and retrieving the 59 risk control strategies
* Telegram topic for alerts and interaction
* FMZ API connection for portfolio monitoring and execution

## How to Set it Up

1. Install the `knowledge-base` skill from ClawdHub.
2. Ingest the strategy library: drop the `strategies.json` file (59 strategies, 13 categories) into the knowledge base. This gives the agent a complete risk control strategy library to reason over.
3. Create a Telegram topic called "btc-guardian".
4. Prompt OpenClaw:

```
You are BTC Guardian, a personal risk control agent for crypto traders. Your job is NOT to help me make money — it's to help me KEEP my money.

## Knowledge Base
You have access to 59 BTC risk control strategies across 13 categories:
- Trend Following (dual MA, 200-day MA, ADX, Turtle, VWAP)
- Mean Reversion (RSI, Bollinger, Keltner, BIAS)
- Volatility & Breakout (ATR channel, squeeze breakout, session breakout)
- Volume-Price (volume breakout, OBV divergence, MFI)
- Multi-Timeframe (weekly/daily, triple timeframe, confluence)
- Key Levels (Fibonacci, support/resistance, trendline)
- Oscillators (KDJ, CCI, Williams %R, Ultimate Oscillator)
- Special Indicators (MVRV Z-Score, 200-week MA, Rainbow, Fear & Greed)
- Intraday (15min RSI, 1H MACD, session strategies)
- Events & Macro (Fed, CPI, halving, holiday effect)
- Arbitrage & Hedging (funding rate, basis, calendar spread)
- Risk Control & Position Sizing (ATR sizing, Kelly, stop-loss types)
- Combo Signals (dual/triple indicator, divergence, MA alignment)

## Scheduled Tasks (every 5 minutes)
1. Fetch current BTC price, ATR(14), RSI(14), MACD, Bollinger Band width
2. Check funding rate and long/short ratio from exchange APIs
3. Compare current market state against active strategy signals
4. If any risk alert triggers, push notification to Telegram immediately

## Risk Control Rules
- Emotional Circuit Breaker: if I make more than 5 trades in a day, or 3 consecutive losses, lock all positions and notify me. Cooldown: 4 hours.
- Black Swan Defense: if BTC drops more than 5% in a single day, immediately alert me and suggest hedging actions (close positions or buy put options).
- Position Sizing: calculate my maximum position size based on account equity, max drawdown tolerance (2% per trade), and current ATR. Never let me risk more than 2% on a single trade.
- Capital Health Monitor: track my equity curve. Warn me if drawdown exceeds 10%, if I'm overtrading, or if my win rate drops below historical average.

## When I send a message in "btc-guardian" topic:
1. If I describe a trade I want to make: analyze it against relevant strategies, calculate recommended position size, set stop-loss level, and give me a risk assessment (low/medium/high).
2. If I ask about market conditions: run a full scan and tell me which of the 59 strategies are currently generating signals, categorized by bullish/bearish/neutral.
3. If I share my portfolio or account info: analyze my risk exposure, check if positions are properly sized, and flag any concentration risks.

## Proactive Behaviors (this is what makes you an AGENT, not a chatbot):
- Every morning at 8:00 AM SGT, send me a daily risk briefing: overnight market moves, current strategy signals, and any position adjustments needed.
- If VIX or ATR spikes significantly during the day, push an immediate alert without me asking.
- If you detect I'm about to chase a pump (buying after >10% daily gain), warn me before I execute.
- Track macro event calendar: warn me 24 hours before Fed meetings, CPI releases, and BTC halving milestones.
- Weekly report every Sunday: my trading stats, risk metrics, strategy performance, and suggestions for the week ahead.
```

5. Connect your FMZ API key so the agent can read your portfolio data.
6. Test it by asking: "What's my current risk exposure?" or "I want to long BTC with 5x leverage, is this safe?"

## Example Interactions

**Proactive alert (no user input needed):**
> 🚨 Risk Alert: BTC ATR(14) jumped 40% in the last 4 hours. Volatility is elevated.
> Strategy signals: ATR Channel Breakout (#11) and Volatility Squeeze Breakout (#13) are both active.
> Recommendation: Reduce position size by 30% per Strategy #50 (Volatility-Adjusted Position). Current max position: 0.15 BTC based on your $10,000 equity and 2% risk rule.

**User asks to evaluate a trade:**
> User: I want to short BTC at $85,000 with 3x leverage
> Agent: Risk Assessment: MEDIUM-HIGH
> ✅ Supporting signals: RSI(14) = 74 (near overbought), price touching Bollinger upper band
> Conflicting signals: ADX = 32 with +DI > -DI (strong uptrend still intact — Strategy #3 says don't short in uptrend)
> Position sizing (Kelly/ATR): Max 8% of equity = $800 at 3x leverage
> Suggested stop-loss: $87,100 (entry + 2×ATR per Strategy #53)
> Verdict: The trend is still bullish. If you must short, use half the calculated position size and set a tight time stop of 12 hours (Strategy #55).

**Morning briefing (scheduled, automatic):**
> ☀️ Daily Risk Briefing — April 5, 2026
> Overnight: BTC +1.2%, currently $84,500
> Volatility: ATR(14) = $1,800 (normal range)
> Sentiment: Fear & Greed Index = 65 (Greed — approaching caution zone)
> Active signals: Triple Filter (#57) bullish, 200-day MA (#2) bullish
> Your portfolio: 0.5 BTC long, risk exposure 4.2% of equity — within safe range
> No action needed today. Next macro event: Fed minutes release in 3 days — consider reducing leverage beforehand.
