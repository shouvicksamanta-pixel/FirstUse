# RSI Divergence Indicator (Pine Script v4)

## Overview
This is a comprehensive RSI (Relative Strength Index) divergence indicator for TradingView that identifies both regular and hidden divergences between price action and RSI momentum. The indicator includes built-in alert conditions and position tracking capabilities.

## Key Features

### 1. **Divergence Detection**
- **Regular Bullish Divergence**: Price makes lower lows while RSI makes higher lows
- **Hidden Bullish Divergence**: Price makes higher lows while RSI makes lower lows  
- **Regular Bearish Divergence**: Price makes higher highs while RSI makes lower highs
- **Hidden Bearish Divergence**: Price makes lower highs while RSI makes higher highs

### 2. **Visual Indicators**
- Color-coded bar coloring:
  - **Yellow**: Long entry signals
  - **Purple**: Long exit signals  
  - **Blue**: Active long position
- Labeled divergence points with clear text markers
- RSI plot with overbought/oversold levels

### 3. **Alert System**
- **RSIDiv BUY ENTRY**: Triggered on bullish divergences
- **RSIDiv BUY EXIT**: Triggered on exit conditions

### 4. **Position Tracking**
- Persistent variable `longPos` tracks active long positions
- Automatic position management with entry/exit logic

## Input Parameters

| Parameter | Default | Description |
|-----------|---------|-------------|
| RSI Period | 5 | Period for RSI calculation |
| RSI Source | close | Price source for RSI |
| Pivot Lookback Right | 3 | Bars to look right for pivot detection |
| Pivot Lookback Left | 1 | Bars to look left for pivot detection |
| Take Profit at RSI Level | 75 | RSI level for profit taking |
| Max of Lookback Range | 60 | Maximum bars to look back for divergence |
| Min of Lookback Range | 5 | Minimum bars to look back for divergence |
| Plot Bullish | true | Show regular bullish divergences |
| Plot Hidden Bullish | true | Show hidden bullish divergences |
| Plot Bearish | true | Show regular bearish divergences |
| Plot Hidden Bearish | false | Show hidden bearish divergences |

## Trading Logic

### Entry Conditions (`longCondition`)
Triggered when either condition is met:
- Regular bullish divergence (`bullCond`)
- Hidden bullish divergence (`hiddenBullCond`)

### Exit Conditions (`longCloseCondition`)
Triggered when both conditions are met:
- Active long position exists (`longPos >= 1`)
- Either RSI crosses above take profit level OR regular bearish divergence occurs

### Position Management
- `longPos` increments on each entry signal
- `longPos` decrements on each exit signal
- Allows for multiple position tracking

## Color Scheme

| Element | Color | Purpose |
|---------|-------|---------|
| Bull Signals | Green | Regular bullish divergences |
| Bear Signals | Purple | Regular bearish divergences |
| Hidden Bull | Light Green (80% transparency) | Hidden bullish divergences |
| Hidden Bear | Light Red (80% transparency) | Hidden bearish divergences |
| RSI Line | Purple (#8D1699) | Main RSI plot |
| Background Fill | Light Purple (#9915FF, 90% transparency) | Between overbought/oversold levels |

## Usage Instructions

### For TradingView:
1. Open TradingView Pine Editor
2. Copy the code from `rsi_divergence_indicator.pine`
3. Click "Add to Chart"
4. Configure input parameters as needed
5. Set up alerts for "RSIDiv BUY ENTRY" and "RSIDiv BUY EXIT"

### Interpretation:
- **Yellow bars**: New long entry opportunity
- **Blue bars**: Currently in a long position
- **Purple bars**: Exit signal triggered
- **Labels**: "PD", "PRD", "ND", "NRD" mark divergence points

## Technical Details

### Pivot Detection
The indicator uses `pivotlow()` and `pivothigh()` functions to identify significant RSI turning points within the specified lookback periods.

### Range Validation
The `_inRange()` function ensures divergences are detected within the specified lookback range (5-60 bars by default).

### Persistent State
Uses `var` declaration for `longPos` to maintain position state across bars without resetting.

## Risk Considerations
- This is an indicator, not a complete trading strategy
- Always use proper risk management
- Consider market conditions and other technical factors
- Backtest thoroughly before live trading
- Hidden divergences can be less reliable than regular divergences

## Version Information
- **Pine Script Version**: v4
- **License**: Mozilla Public License 2.0
- **Author**: © mohanee

## Label Meanings
- **PD**: Regular Bullish Divergence (Price Lower Low, RSI Higher Low)
- **ND**: Regular Bearish Divergence (Price Higher High, RSI Lower High)
- **PRD**: Hidden Bullish Divergence (Price Higher Low, RSI Lower Low)
- **NRD**: Hidden Bearish Divergence (Price Lower High, RSI Higher High)

## Customization Options
The code includes several commented sections that can be uncommented for additional features:
- Alternative bar coloring schemes
- Strategy entry/exit functions (currently commented out)
- Additional visual markers for entry/exit points