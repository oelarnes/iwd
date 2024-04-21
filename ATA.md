We’re taking a break from GIH WR to discuss one of my pet topics: pick orders. The observed ones, ALSA and ATA. Your picks are valuable, and the observations about what people spent on cards are relevant to the card quality question.

*You have to know your pick orders.* It’s a truism, one of the first pieces of advice you get as a limited player. But I still don’t think ATA gets the respect it deserves. Instead, the attitude I observe is something like “it’s important to know ALSA so you know when you have to take quality cards,” and quality is identified with the performance metrics. I believe this is a mistake. 

Quick recap of what the acronyms mean: ALSA is “average last seen at”, which I think of as a market price. It’s the price you have to pay on average to draft a card. It’s the more principled stand-alone metric. ATA is “average taken at”, which is where 17l drafters actually took their card in the recorded data: Price paid. Because this data is coupled to the win rate data, if you want to combine them as I suggest below, you should use ATA. But also it doesn’t really matter, the rankings are basically the same.

Let me start with an analogy: Suppose you’ve decided to get started in Magic finance. You do a lot of research on the rarity, function, and trends in popularity of different cards in different formats. You even get access to profitability data and you see what cards made sellers the most money in the past. You devise a price model and put price stickers on your cards and see what happens. There’s just one problem: you didn’t look at the market. Well, you’re going to get wiped out. Your underpriced cards will get snapped up and your overpriced cards will languish. You’ll have to restock at a loss. You can’t operate like that. In markets, we intuitively know that price is the starting point for value. If you’re looking for value, it is always relative to the market. A find is either underpriced or overpriced. *You have to know the market.*
## The Draft Marketplace
Drafting costs money. You pay your money and in return you get 39 picks. Three first picks, three second picks, and so on down the line. Those are your picks and each pick had a different price. Obviously you paid more for your first picks: if you could trade them with other players you might trade a first pick for a 2 and a 4, but probably not a 2 and a 7. You might trade your whole wheel for another early pick. So there’s some price S_n for each of the n picks 1 through 13 that decreases as n increases. If you’re worried that the pick values differ between packs, just average them over packs one through three.

First, another analogy: Each draft pick is like a store where everything is the same price. Everything costs $1, or whatever. Now suppose you can put price stickers on each card showing the price that other people paid for them. If you didn’t know anything else, you’re grabbing the card with the highest price sticker every time. ATA is the price sticker.

 When you draft you are trading your picks for cards. You bought all your picks for B, your buy-in. Looking at any particular card C taken at position n, we spent S = S_n on that pick. With the *major and unfounded* assumption that the value of the rest of our pool is independent of C taken at n, whether you’ve drafted the other cards yet or not, we have effectively B-S to spend on the rest of our deck.

Now we’re going to achieve some win rate WR based on that choice: that pick at that price, on average. How many wins can we achieve with a card C and B-S dollars? Clearly if we can spend more money, we can buy more wins. *An extra Shock would look pretty nice here, right? Let’s go shopping.* If WR(C, S) = WR(D, T) for two cards C and D at two different costs S < T, then it must be the case that WR(C,S) < WR(D,S). Give the D player more money, and they can buy more wins. If you can buy a card below market rate, you will be able to capture more wins than the win rate data suggests.

If we can price picks in terms of win rate, then under a linearity assumption, this is a complete model. Add the price paid to the win rate and you have a position-invariant measure of card quality. Let Q be the wins you can buy with the rest of your pool, and let MRW be the marginal win rate you get by adding C to your deck (I know, I know) then WR(C,S) = MWR(C) + Q(B-S) = MWR(C) +Q(B) - Q(S), and Q(B) is constant, so WR(C,S) + Q(S) is constant in S. Furthermore MWR(C) = WR(C,S) + Q(S) plus a universal constant.

So this great, and I am sure that we really want to do this, but of course there are loads of unanswered questions. For one thing, can you add wins like that? Well of course not, but also, yes. Swap a Vindicator for a filler white common in a typical limited deck, and yes you are going to add a predictable number of wins on average. As long as we operating in the marginal space around typical limited play, I feel comfortable with the linearity argument. This is the premise of rankings anyway. Everyone knows about synergy and context and nuance. We know your 23rd card gets better as your deck gets better. We still need a ranking, and linearity assumptions helps us build that ranking. That’s what you’re doing when you value one win rate number over another in the context of 39 other cards. Just don’t go around trying to build a model starting from 0% or getting up to 100% (or beyond!).

Nonlinearity is not the torpedo that’s going to sink this ship, it’s measurement bias.

Before we get to that let’s take a step back and see what we are saying.

**The quality of a card is the sum of the observed win rate based on where it was picked plus the price of that pick** (measured in the win rate you could buy for that price). You cannot measure card quality without looking at observed pick orders. Win rates by themselves are not card quality.

Now, that’s all well and good and theoretical, but can we measure it? If the curve is flat anyway, then it’s academic. We will get to a measurement (it’s not flat), but that measurement is plagued by bias questions that are impossible to answer with the current state of technology (unless you are Ryan Saxe), since they hinge on questions of strategy and synergy. So first I want you to do an exercise. Write down some prices.

Imagine a stip draft with a stickered d100. It has k stickers on it that say “win”. You can take the die and you get roll it after each game whether you win or lose, and you get a free win on a sticker either way (a pack or whatever, don’t get hung up on how this affects arena bo1. The idea is it increases your win rate by k%), but in exchange I’m going to make you pick one of your first picks right into the trash bin. I’ll tell you which one later. Think of your price. Are you taking 1%? 2%? 3%? We do love our first picks…

Now think about the shape of that curve if I make you trash an nth pick instead. We’re just talking about one pick, one die, so don’t worry about making playables. Of course feel free to use decimals.

Ok, you have your model, and you can map ATA to that and add it to GP WR (actually you want as-picked WR, but shrug). Really, it works, try it!

Now let’s look at the data.
## Win Rates Increase with Pick Number
Under our (bad) independence assumption, we can observe WR(C,n) directly by seeing how many wins were obtained with C and the rest of the buy-in. In other words, we want to chart as-picked win rate vs the location a card was picked at. Since WR(C,n) + Q(S_n) is supposed to be a constant measure of card quality, and Q is supposed to decrease in n, WR should increase in n, and the rate of increase should tell us the rate of decrease of Q. We can grab all of this data straight from the public draft data file on 17lands.com. 

Lets look at pictures! This is exactly the chart described above for some white commons. The dot is the center of mass of the line, the (ATA, As-Picked WR) point.

![[Pasted image 20240415092925.png]]
Line goes up! Stonks! We did it! And the slopes look reasonably similar. Maybe a bit of good luck there, or systemic similarity, because in general the shapes can be quite noisy. But I didn’t cherry-pick this one, it has the cards I wanted to look at first. Cards with different functional profiles have different shapes (generally related to how they interact with synergy and who favors them based on skill level).

So broadly, we are observing that the earlier you take a given card, the lower your win rate. You spent more on it. If you first picked a Marketwatch Phantom, that means (under our assumptions) that you didn’t get a “real” first pick, and your win rate suffers as a result. If you got it late, you got to add it to a deck with more quality cards.

Now take a look at Phantom vs Seasoned Consultant. Phantom dominates Consultant over the heaviest and least noisy parts of the curve, picks 3 through 7. In any particular pack, you are better off taking Phantom. I mean you know that already. It’s the better card. But Seasoned Consultant has a higher win rate, because it is cheaper and people have more valuable picks to spend on their decks when they take it on average. The win rate data is not wrong, it’s just incomplete. Add the prices back in, and you get the correct order.

Now let’s check the GIH WR of Marketwatch Phantom. It’s 55.5% over this data set, rank 113/296. That ranking is too low. Way too low. I have it rank 62 on my chart, but whatever: It’s a strong early pick. That difference understates how bad the ranking is because many of the cards above it are rares and mythics and many of those in between are commons. We saw last time that GIH disfavors it because it’s an aggro card. Now we are seeing it is disfavored because it’s an early pick and has a harder time building win rate. Next time we will see it’s disfavored because its appearance in a deck is correlated with consistent deckbuilding.

In order to correct for that, we have to price Q in wins.
## Pricing a pick
We’re going to slight tweak the formula here to MWR(C) = WR(C, n) + Q(n), dispensing with the price conceit. Just converting pick order to wins. Then take the derivative in n and we get Q’(n) = -WR’(C, n). The slope of each card graph should estimate the slope of Q. Since rates are linear, we can just average them over all the cards to estimate the underlying rate. There’s some important nuance to weighting that I won’t bore you with, but it’s something to be aware of if you want to try yourself. Anyway, with some weighting of cards based on where and how often they are picked, we get the following graph of Q’:

!!!!Graph Here!!!!

It’s negative, and it decreases in magnitude. That makes sense! Going from a first pick to the second pick, you give up the best card in the pack. That’s worth a lot! Going from 10 to 11, you give up something, but a lot less. There’s no particular reason to see a trend other than linear here (something I got wrong in my earlier models), so let’s just fit a line to it:

!!!!Model Here!!!!!

Now integrate, and we have a quadratic model of pick value. We can plug ATA in, and since it’s not too far off linear, it won’t be a big deal that ATA averages some nearby values. If the price of a 13th pick is zero (an arbitrary baseline), then a first pick is worth 2.4% in win rate.

In the future we will chat about what it looks like when you start adding things together, but first we need to discuss why this is wrong and what to do about it.
## Selection Bias
When you segment observations by some variable (pick order) in order to observe a trend in another variable (win rates), you may also be segmenting the population by other variables (skill, pool synergy, pool quality). If those variables are correlated with winning, then that will obfuscate the trend you want to observe. We saw that last time, where we counted card appearances, which were correlated differently with win rates depending on the card. This effect is broadly called selection bias, and can have a disruptive effect on the quality of a model.

Let’s go through some relevant biases to see how they affect our model.

First skill bias: If drafters of higher skill tend to take a card earlier, that will bump up the front end of the curve. If drafters of lower skill take a card earlier, it will depress the front end. The key thing here is we are averaging over all cards with appropriate weights. On average, both high and low skill players take some cards early, and some cards late. I don’t think there is a first order effect here to worry about.

Same thing for pool quality. Some cards might be taken early in high quality pools, others in low. On average, that should balance out.

Pool synergy is a different story. On average, people whose pools synergize with the card in question will take it earlier. I mean duh, that’s the whole point of drafting. That will boost the front end of the curve, more for later packs than early ones. This effect is especially visible in good cards like On the Job that wheel frequently. At picks 12 and 13 the win rate dives back to set average because the card is going to a random drafter. This is true to greater or lesser extent among cards, but the effect should always point in the same direction: to dampen the pick value signal.

My personal view is that the way to correct for this is to rely on the trend in pack one, when synergy has less impact on pick orders. If you’re not convinced by this argument, or if you feel that pack one is inherently more valuable, then you may not want to use this number and that’s ok. Here’s the graph and model for pack one:

!!!New Graph!!!

Not bad, right? I wrote this text before I did the analysis, so if the text is still here, which it is, that means I predicted the trend acceptably well. It’s like 3.5%, right? No? Hopefully that gives more weight to my argument. Don’t worry, I’ll let you know if I got it wrong. But I didn’t. Well, except the number is XXX not 3.5.

So in conclusion, a first pick is worth (maybe) between 2.4% and XXX. (Or more)

You need to be looking at ATA to value cards using 17lands data.

Next time we will use these numbers to decompose GIH WR further to isolate an additional source of bias. Thanks for reading and please ask questions!

