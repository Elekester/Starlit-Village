# Optimizing Augment Capsule Use in PSO2: NGS

When adding augments to your weapons and armor, it is more efficient to spend 1 capsule per augment than 10 capsules per augment if you have a boost to Augmentation Success Rate through an event or item. To make best use of the boost and your time you can still do separate augments simultaneously, just don't spend more than 1 capsule per augment type on an attempt.

## Details

When adding augments to your weapons and armor, you're provided with the option to use up to 10 capsules on an augment at once. The success rate of that augment is then the success rate of a single capsule times the number of capsules. That means you can save time and money by spending 10 capsules at once instead of trying to augment them one capsule at a time. On average you'll end up spending the same number of capsules, even accounting for failures. However, this is only true if your Augmentation Success Rate is not being boosted.

If you have even just a +5% Augmentation Success Rate Boost from an event or item you can use about two-thirds of the capsules by attempting to add augments 1 capsule at a time. This is because that boost is only added once if you spend 10 capsules at once, but added each time if you spend 1 capsule at a time, effectively increasing the boost you receive. Notably, the variance is increased significantly when augmenting 1 capsule at a time. It's very possible that you end up spending more capsules than you would otherwise.

The savings increase if you have greater boosts or if your attempting to add augments with lower success rates. By just spending a +10% Augmentation Success Rate Boost you'll save 61% of your capsules on average when attempting to add a Halphinale augment for example.

The downside of 1 capsule Augmenting is the massive varianc it introduces. While it will be better than 10 capsule Augmenting 87% of the time with a +10% boost, the other 13% of the time you'll spend more capsules. Potentially many more capsules.

## Supporting Data

![Supporting Data](/Images/Augmenting_Method_Stats.png)

\* Averages and Standard Deviations were calculated using the geometric distribution. The probabilities were calculated using simulations using the below code.

```python
from random import random
from math import sqrt

def num_capsules(capsules, true_odds):
    count = capsules
    while random() >= true_odds:
        count += capsules
    return count

def num_capsules_average(capsules, odds, boost, n):
    true_odds = capsules*odds + boost
    sum_ = 0
    sum_squares = 0
    for x in range(n):
        count = num_capsules(capsules, true_odds)
        sum_ += count
        sum_squares += count**2
    return sum_/n, sqrt((sum_squares - sum_**2/n)/(n - 1))

# This function generates the averages and variances, for each Success Rate and Boost combination.
def num_capsules_table(capsules = 10, n = 1000):
    odds_list = [0.05, 0.06, 0.07, 0.08, 0.09, 0.1]
    boost_list = [0.0, 0.05, 0.1, 0.15, 0.2, 0.25, 0.3, 0.35, 0.4]
    string_1 = "Average for {} caps: \n".format(capsules)
    string_2 = "Standard Deviation for {} caps: \n".format(capsules)
    for odds in odds_list:
        for boost in boost_list:
            average, variance = num_capsules_average(capsules, odds, boost, n)
            string_1 += "{}\t".format(average, 1)
            string_2 += "{}\t".format(variance, 1)
        string_1 += "\n"
        string_2 += "\n"
    print(string_1)
    print(string_2)

# This function generates the probabilities of two different methods of augmenting, for each Success Rate and Boost combination.
def comparison_table(capsules1, capsules2 = 10, n = 1000):
    odds_list = [0.05, 0.06, 0.07, 0.08, 0.09, 0.1]
    boost_list = [0.0, 0.05, 0.1, 0.15, 0.2, 0.25, 0.3, 0.35, 0.4]
    string = "Probabilty {} capsules better than or equal to {} capsules:\n".format(capsules1, capsules2)
    sum_ = 0;
    for odds in odds_list:
        for boost in boost_list:
            for x in range(n):
                true_odds1 = capsules1*odds + boost
                true_odds2 = capsules2*odds + boost
                if (num_capsules(capsules1, true_odds1) <= num_capsules(capsules2, true_odds2)):
                    sum_ += 1;
            average = sum_/n
            string += "{}\t".format(average, 1)
            sum_ = 0
        string += "\n"
    print(string)

num_capsules_table(10, 1000000)
num_capsules_table(1, 1000000)
comparison_table(1, 10, 1000000)
```
