+++
title = "Sports Betting Strategy"
date = 2025-09-01
+++
# Sports Betting Strategy
Sports betting goes back thousands of years and has long been a pastime for sports enthusiasts. 
Unfortunately, it can turn into an addiction, or be the precursor to financial ruin for many individuals. 
Recently, I have developed an interest in statistics-based sports betting. I compare it
to something like counting cards in a casino. Not illegal, but you will be limited very quickly when Vegas finds out.

## Sports Betting vs. Stock Market
Sports-betting has shocking similarity to the stock market
in more ways than one. Both have strategies for winning, yet nobody knows the real result until it happens. 

Since my focus as a developer is in the algorithmic side of either trading or betting, I noticed that many of
the strategies for either market remain largely the same, with a common emphasis on statistics.

The reason I highlight this comparison is to explain that I am not just throwing money away, and that responsible or informed gambling can be equally profitable.
I could also use this to poke fun at stockbrokers but I'll leave that to you. (Gamblers in suits)

## Statistics in Sports Betting
Now that I have mentioned that there *are* strategies for applying stats in sports betting, I should probably explain what they are.

The fundamental concept for any type of wager is **expected value**. If you have taken a stats class already I will remind you that it is
a weighted average of all possible values of a random variable. If you have not taken a stats class, consider the following:

You are offered a bet on a fair coin flip. If it is heads, you win \\$10. If it is tails, you lose \\$5.
You know that the probability of it being heads is 50\% and tails is also 50\%. You then multiply the 
probability of each outcome by the value obtained from that corresponding outcome. In this case:

$$ 0.5 \times $10 + 0.5 \times -$5 = $2.50 $$ 

This means that every time you play, you are expected to win \\$2.50. If you played 100 times, you'd expect about a \\$250 profit in the long run.

Expected value is the backbone of smart sports betting. I will reference it many times in subsequent sections.

## What are the True Odds?
Your next question may be, "how can you get the *real* probabilities of some type of sports bet?". The short answer is there is no answer. There will
never be an exactly correct probability of a certain outcome. In practice, there are a variety of methods to developing a *fair* line. I will outline a few.

### Consensus Line
One approach you could take is to average all odds for a specific bet into an "average" line. This may give you a solid baseline for what most sportsbooks
are asking for, but it is important to acknowledge two critical pieces of information. The first is that there are fewer oddsmakers than you realize. Often times
sportsbooks will just react to an industry-standard oddsmaker, instead of determining a fair line themselves. The second is that some sportsbooks are better 
at setting fair odds than others. 

### Sharp vs Non-Sharp / Soft Sportsbooks
You can often tell how good a sporstbook is at setting odds by how much they limit their users. A sportsbook like Pinnacle is referred to as "sharp", because
their lines are extremely competitive and they don't limit winning players. Think of a casino that does not kick you out for counting cards. They make their money
through tiny margins in the odds called "vig", so they have an advantage in the long run.

On the contrary, many sportsbooks cater to your average joe (not a professional gambler). In these cases, they will limit you if you start to win too much money.
This is often because they are slower to adjust their lines or they focus more on entertainment than line accuracy. 

### Sharp Sportsbook Consensus
This brings me to another solution to finding the fair line - the sharp sportsbook consensus. Instead of averaging the lines of *all* sportsbooks, you just average
the most statistically-accurate books. This gives you a better representation of the true odds, because many sharp sportsbooks change their lines in response
to small details about the game like whether the pitcher tweets about wrist pain before the game. This will likely be the best way to determine a fair line.

Now that you know where to get the data to determine a fair line, let's talk about how to actually calculate it.

## Odds Conversion and Removing Vig
Remember vig? We need to get rid of that small margin to determine the true odds of the outcome. The odds that they give you *can* be converted into percentages,
but they will be skewed by vig, so we must remember to remove it. Consider the following example:

Using American Odds: Team A has a line of -130 and Team B has a line of +120.

**Step 1** is to convert the American Odds to their implied probabilities: 

Team A (negative): $$ p = \frac{a}{a + 100} = \frac{130}{130 + 100} = 0.565217 $$
Team B (positive): $$ p = \frac{100}{b + 100} = \frac{100}{120 + 100} = 0.454545 $$

If we sum these odds we notice that $ 0.565217 + 0.454545 = 1.019763 $. That extra few decimals over 1.0 is the vig. 

**Step 2** is to remove this from our calculation. We accomplish this by *normalizing* it to 100\%. 

$$ p_{fair^A} = 0.565217 / 1.019763 = 0.554264 = 55.4264\\% $$
$$ p_{fair^B} = 0.454545 / 1.019763 = 0.445736 = 44.5736\\% $$

Congrats! You now have a probability of each outcome without the margin. You can now leverage this information in your future bets.

## Placing the Bets and Limitations
Now that you have an accurate probability of the outcomes, you can calculate the expected value and determine if you will face long-run success.
However, there are a few roadblocks you will face.

- Lines are recomputed often and can affect your calculations. Take care in confirming your calculations are still relevent when you place a slip.

- If you win too much, many sportsbooks will limit you. Beware of this and factor it into your strategy.

- Some sportsbooks are softer in specific sports or markets. Do some research to find which ones may expose an edge for you.

- You **will** lose, have trust in the long-run effects. Many parlay strategies have around a 20\% win rate. Winning 20\% of the time does not sound
great but you **must** hold out, and you will have success over time.


Good luck and enjoy!
