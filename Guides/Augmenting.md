# Optimizing Augment Capsule Use in PSO2: NGS

## The Two Methods

When adding augments to your weapons and armor, you're provided with the option to use up to 10 capsules on an augment at once. The success rate of that augment is then the success rate of a single capsule times the number of capsules. That means you can save time and money by spending 10 capsules at once instead of trying to augment them one capsule at a time. On average you'll end up spending the same number of capsules, even accounting for failures. However, this is only true if your Augmentation Success Rate is not being boosted.

If you have even just a +5% Augmentation Success Rate Boost from an event or item you can use about two-thirds of the capsules by attempting to add augments 1 capsule at a time. This is because that boost is only added once if you spend 10 capsules at once, but added each time if you spend 1 capsule at a time, effectively increasing the boost you receive. Notably, the variance is increased significantly when augmenting 1 capsule at a time. It's very possible that you end up spending more capsules than you would otherwise.

The savings increase if you have greater boosts or if your attempting to add augments with lower success rates. By just spending a +10% Augmentation Success Rate Boost you'll save 61% of your capsules on average when attempting to add a Halphinale augment for example.

**However**, we've ignored the variance introduced by the second method.

## Supporting Data

![Supporting Data](/Images/Augmenting_Method_Stats.png)

\* The probability was calculated treating the two distributions as normal distributions with
