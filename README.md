# Kelly Criterion Simulation

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Estherj22/kelly-criterion-simulation/blob/main/kelly_simulation.ipynb)

A Python Monte Carlo simulation of how much of your bankroll to bet when you have an edge. I built it to understand why over-betting destroys growth even when the odds are in your favour.

## The question

If you can repeatedly bet on a game where you have an advantage, what fraction of your bankroll should you stake each time? Bet too little and you grow slowly. Bet too much and a few bad streaks ruin you.

## How it works

- **The game:** a coin that wins 55% of the time and pays even money.
- **The Kelly fraction:** f = (b x p - (1 - p)) / b, which is 0.10 here, so bet 10% of the current bankroll each round.
- **The simulation:** 1,000 independent players each make 1,000 bets, always staking a fixed fraction of their current bankroll.
- **Strategies compared:** half Kelly (5%), full Kelly (10%), double Kelly (20%) and a reckless 50%.
- **What I measured:** median final bankroll, share of players who ended below where they started, median worst drawdown, and growth rate per round compared with the theoretical formula.

All data is simulated, so there is nothing to download.

## Results

![Median bankroll for each bet size](kelly_growth.png)
| Strategy | Median final bankroll | Ended below start | Median worst drawdown |
|---|---|---|---|
| Half Kelly (5%) | 4,263.2 | 0.8% | 62.0% |
| Full Kelly (10%) | 18,291.8 | 4.4% | 89.3% |
| Double Kelly (20%) | 87.1 | 52.8% | 99.9% |
| Reckless (50%) | 0.0 | 100.0% | 100.0% |

**Finding 1:** Full Kelly (10%) grew fastest, turning a bankroll of 100 into a median of 18,291.8. Its simulated growth of 0.0052 per round was close to the theoretical 0.0050, and the other three strategies matched theory exactly at four decimal places, so the simulation agrees with the formula.

**Finding 2:** Half Kelly gave up some growth for much more safety. Its growth rate (0.0038) was roughly three quarters of full Kelly's, but only 0.8% of players ended below their start, against 4.4%, and the median worst drawdown was 62.0%, against 89.3%. Even at full Kelly the typical player lost almost 90% from a peak at some point, which is why traders often bet a fraction of Kelly.

**Finding 3:** Betting double Kelly (20%) removed all the benefit. Growth was about zero (-0.0001), the median player finished at 87.1, below the starting 100, and 52.8% of players lost money. At 50%, all 1,000 players lost money and the median bankroll was effectively zero, even though every single bet had a positive expected value.

## Limitations

- The win probability is known exactly, whereas real edges are uncertain and change over time.
- Bets are independent and the payout never changes.
- There are no trading costs, and bankroll can shrink without limit.
- A fixed fraction ignores that real bettors have limits on how much they can stake.

## Run it yourself

1. Click the Open In Colab badge at the top, or download kelly_simulation.ipynb and open it in Jupyter.
2. Run all cells. The settings at the top of the code let you change the win probability, odds and bet sizes.

## Possible next steps

- Cap the maximum drawdown and measure what it costs in growth.
- Bet on two independent games at once and split the Kelly fraction between them.
- Add a cost per bet and find the smallest edge that is still worth betting.
