This is part 2 of my series analyzing the widely used metrics on 17lands.com. In part 1 I quantified the control bias inherent to the way GIH WR is measured. It wasn’t pretty. Today I want to look at what we lose by discarding GNS (not seen) WR.
## Gravity 

*Let C be some card…*

The assumption behind GIH WR is that the not-seen data is essentially noise, or worse yet, *bias*. I mean, we’re literally throwing it out, so it must be worthless. What’s the idea of GNS? It’s looking at the games where you don’t draw a copy of your particular card C, so, after correcting for control bias, it should look very much like a GP WR for a 39 card deck missing one copy of the C. The argument for throwing it out goes something like, “we want to boost the signal of C so we’re going to throw out some of the data for the other cards around it.”

First of all I need to explain how we’re going to use GNS WR and think about it. I need one simplifying assumption:

GIH WR = 2 x GP WR - GNS WR.

Now, this isn’t exactly true. But it really is close enough for our purposes; it’s just a matter of how the marginal signal from the seen and unseen parts of the deck are weighted^1. This article got way too long when I tried to explain everything, so I’m going to make some marks and add supplementary information in a comment. If you believe in what I’m doing, you can skip them, if not I hope you’ll take a look.

That double GP WR component is going to loom over the whole argument like a turn 3 Vein Ripper. Anything we want to add to that had better be stripping away bias from GP WR or adding new sources of equity. At the end, if we haven’t improved on that signal, and indeed if we’ve mucked it up with bias, then we’re better off using GP WR instead.

We want to understand the quality of those 39 cards and how they might bias our GP WR evaluation, so let’s look at another way to measure them. What I’d like to do is take an average decklist containing C, minus one copy of C, and average all of the GP WRs for those 39 card bits. This metric will be called D1WR, for “distance-one win rate” (Distance in the sense of an adjacency graph). See below how to calculate D1WR^2.

From a card quality signal point-of-view it’s close but not quite the same thing as GNS. It contains a bit extra of every other card in the set, and a bit less of the 39 particular cards. We will keep that in mind when we look at the data, but my expectation is that this effect is extremely minimal, and more importantly it will shift that card quality question into the residue term at the end of the analysis.

But D1WR does something else important. It gets rid of the gravity that C imposes on the GNS decklist. If you built around C, or played a worse mana base then average, or played a color combination that performs worse than the card quality should imply, then that is going to reduce your GNS relative to D1WR. If C is correlated with playing a good color combination or a good creature curve, then that will increase GNS relative to D1WR.

Let GNS* = GNS WR - Deck NSD (not-seen difference, or just the opposite of Deck IHD given our assumption), and let Grav = D1WR - GNS*. C is sucking wins out of the rest of the deck, so gravity, right? Sounds cool enough. Now we’re going to insert our term into the GIH breakdown:

GIH WR = GP WR + Deck IHD + Grav + (GP WR - D1WR) = GP WR + Deck IHD + Grav + D1D.

This last term, “D1D” for “distance-one delta” is where (in my opinion) the juice of GIH WR lies, such as it is, the promised source of marginal equity. But first we need to dispense with Grav.

Weighted by game counts (going forward all statistics summed over card names will be weighted by game count whether I say so or not), Grav has mean 0.0% and standard deviation 0.9%; it has a negative correlation with GP WR and D1D and a significant positive correlation with Deck IHD. Having a negative correlation with GP WR is not a bad thing; after all, what we are looking for is a bias component in GP WR, so it’s not supposed to be correlated. What we need to do is reason about the metric using our knowledge of Magic: the Gathering and consider whether this measures a source of marginal equity in our draft valuations relative to GP WR by itself.

Let’s look at some cherry-picked values of Grav:

Smuggler’s Copter: -1.1%

Dog Walker -0.8%

Torch the Witness -0.6%

A Killer Among Us 0.1%

Repulsive Mutation 0.5%

Incinerator of the Guilty 1.1%

Cryptic Coat 1.7%

Magnifying Glass 2.4%

Vein Ripper 3.2%

Niv-Mizzet 4.7%

The full list will be showng in the output of a notebook file which will be linked in a comment.

## Bias and Equity

Now, is this a marginal equity signal above GP WR? What do we even mean by that? We have to be extremely careful. I got it wrong several times trying to write this up, and it’s still a gray area. These are win and loss events from games of magic running the card in your deck, so they are already a (negative) component of GP WR. They have been effectively doubled under our assumption, but so has GP WR. So there are essentially four cases we have to consider.

1. The value is telling us something about the marginal win equity resulting from the drafter’s valuation of C. That signal looks the same regardless of whether C is drawn. (symmetric signal)
2. The value tells us something about the quality of C, and that signal changes depending on whether or not C is drawn. (asymmetric signal)
3. The value results from circumstances unrelated to the quality of C, unrelated to the drafter’s valuation of C. It is bias, but it has the same value whether or not C is drawn (symmetric bias)
4. The value is bias, but only manifests when C is not drawn. (asymmetric bias)

The gold standard is number 4. If we can locate asymmetric bias and subtract it off, then we are boosting the legitimate signal of GP WR. That’s why I am shifting the marginal card quality question to a different term. There’s an argument to be made that part of that is bias. You shouldn’t be punished for having different preferences when your pool is low quality. 

The symmetric cases are irrelevant, they don’t affect the metric as compared to straight GP WR. But if we are subtracting off an asymmetric signal, then we are doing ourselves active harm. We are failing to measure the results of our choices. So let’s see if we can find a justification for locating asymmetric bias.

Let’s look at Magnifying Glass first, which reminds us of two important things. First of all, Grav is measuring losses, not wins. The marginal losses beyond what the card quality of the rest of your deck would suggest. Second, this is correlation, not causation. Picking and playing Glass is not causing us to lose 2.4% more game when we don’t draw it, it’s a choice that is made by unskilled players and players with trainwreck pools, and those things are correlated with losing whether you draw Glass or not. Verdict: A bit of symmetric signal, due to valuing Glass reflecting poor choices, and significant symmetric bias.

Wait, why are we adding losses again? Well, we’re adding them back because we don’t think they’re relevant. Somehow we have to believe that we can keep the (hidden elsewhere) wins and throw out these losses.

Let’s take a look at Cryptic Coat. People playing Coat are losing 1.7% more of their games when they don’t draw it than their card quality would suggest. Why? I think it’s easy to understand. People are splashing it. They are first picking it out of pack two or three and splashing it at some cost to consistency. *They are right to be doing that.* Coat has magnificent win rates. It’s an A+. Does that mean we should throw out the part of the data that shows the cost of prioritizing it?

Well, if we can reliably capture the wins and avoid the losses, then maybe. How would we do that? By not splashing Coat. By passing it when we open it off color. By treating it as a Sprite. In other words, by deprioritizing it and bringing it down our pick orders. But how are we supposed to do that if we’re throwing out the information that would bring it down our rankings? Personally, I doubt whether there is a secret sauce to playing Coat every time without sacrifice.

Verdict: Asymmetric signal.

I’d love to hang out and chat about Smuggler’s Copter. What a chad making our deck better even when we don’t draw it. But your patience is already wearing thin, so let’s finish up by talking about Niv.

For the record, I am a Niv believer. I trophied with a double-Niv, double-Aurelia deck in Plat 1. In a separate draft I dealt 14 and drew four cards off a solved Case. I won at a better rate with Niv in my deck than without.

But let’s be real. You are not playing Niv-Mizzet, Guildpact without sacrificing consistency. On average, people lost 4.7% more games when they didn’t draw it than card quality would suggest. It’s freaking WUBRG people. You’ve got unsolved Cases sitting around, you’re casting mana fixing on turn 3, it’s a disaster. Are you really suggesting we throw that data out?

But, top players! Its true! Top players do better when they don’t see their Niv. That’s a property of the top player data. If you are a top player, you think you understand how to build a Niv deck, and you want a more nuanced cut that reflects your knowledge, thats what you should look at. But that information is not in the 4.7%. To prove it, check out Cryptic Coat. Grav goes up for top players! That’s (presumably) because they know how good it is, and they are better at estimating how much consistency to sacrifice.

You may very well have the secret sauce. It’s your edge over the broad public. We are not going to find it in this data set. We shouldn’t try. Going back to the idea of finding equity in the draft choices of the broader community: on average, people threw away equity when they drafted Niv, and the rankings should reflect that. If you want a ranking that reflects the card quality you personally experience based on your skill, that’s what the tier list function is for. If you want a ranking that reflects the optimal choices at every stage with perfect play, we have to wait for Gleemax to usher in the singularity.

Verdict: Asymmetric signal

Grav is not bias. Adding it is not a way to boost the equity signal. It might be correlated to equity, and it might not. It might have clues to sources of bias, and it might have clues to ways to find an edge. But it is not inherently that information. Inherently, it’s a shell game, a way to shift losses from one column into another.

Another brick in the wall.

Next time we will break down GIH WR into pieces and see what’s left over (not much).
