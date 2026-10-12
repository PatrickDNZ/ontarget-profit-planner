# OnTarget Profit Planner

A single-file web app for planning an accounting practice's profit. Enter last year's results, set targets for ten profit drivers, and see how much each change adds to (or takes from) net profit.

It is a rebuild of **OnTarget 2000** (RAS, 1999), a Windows 98/XP-era planning tool. The original no longer runs on modern Windows. The formulas here were recovered from the original program, so the results match it.

## Using it

Download `index.html` and open it in Chrome, Edge, Firefox or Safari. There is nothing to install, and it works offline (fonts fall back to system fonts).

The screen follows the original program:

- **People Power, Fees & Rates, Costs** tabs: each driver shows its base value, a slider with −/+ buttons, the target and its profit impact, plus a table of the figures it affects.
- **Base Values**: last year's people, productivity, costs, and WIP and fees. Leave any one WIP field blank and click Calculate to fill it in.
- **Report**: the printable summary (profit drivers with % impact, and outcomes).
- **Action** and **Help**: ideas for reaching the targets, and definitions of every term.
- **Client Statistics**: this tab was on the original screen but was never connected to any calculation. It is kept for layout only.

Base Profit, Targeted Profit and Additional Profit stay visible at the bottom of every tab.

### Saving

**Save** keeps scenarios in your browser's local storage, on that computer and in that browser only. Use **More › Export backup** to save them to a `.json` file, and **Import backup** to load them on another computer. **Reset** puts every target back to its base value.

The app starts with one example scenario, **Sample**. **More › Restore the Sample scenario** brings it back if you change it.

## The model

```
Total people   = partners × (1 + leverage)
Hours charged  = total people × time available per person × productivity
Net fees       = hours charged × hourly rate × disbursement factor × value index × billing index
Total costs    = average cost × team members + variable cost × hours charged + fixed costs
Net profit     = net fees − total costs
```

The ten drivers are partners, leverage, time available per person, productivity, hourly charge rate, value index, billing index, average cost per team member, variable cost per charged hour, and fixed costs.

Rules carried over from the original:

- **Profit impact** is worked out one driver at a time in a fixed order: partners, leverage, time, productivity, rate, value index, billing index, average cost, variable cost, fixed costs. Each impact is the change in profit at that step, so the impacts add up to the additional profit.
- **Changing partners** keeps the number of team members the same unless you also set a leverage target.
- **A target within 0.005 of its base value** counts as unchanged, so rounded figures don't create phantom impacts.

One change from the original: it ignored Value Index and Billing Index targets within 0.5 percentage points of base (a rounding tolerance applied to the wrong units). This version only ignores genuine rounding differences.

## Disclaimer

This is an independent rebuild for personal use. It is not affiliated with or endorsed by RAS, and contains none of the original program's code, help files or data.
