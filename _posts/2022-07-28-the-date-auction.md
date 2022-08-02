---
layout: post
---

# Table of Contents
1. [Introduction](#introduction)
2. [Explanation of First and Second Price Auctions](#explanation1)
    1. [First Price Auction Derivation](#firstprice)
    2. [Second Price Auction Derivation](#secondprice)
3. [Dating Auction Derivation](#datingauctionderivation)
4. [Dating Auction Characteristics](#datingauctionanalysis)
5. [Dating Auction Simulation](#datingauctionsimulation)
5. [Happily Ever After](#happilyeverafter)

# Introduction <a name="introduction"></a>

Disclaimer: I don't take any responsibility for the conversation that comes up 
when you start talking about this with your significant other. :P

Once upon a time there were a pair of people and they were destined to meet and 
live a beautiful life together. There was only one snag... The way they met was 
through a <a href="https://en.wikipedia.org/wiki/Charity_dating#:~:text=Charity%20dating%20is%20a%20process,value%20in%20such%20a%20date.">dating auction</a>. The dating auction is a 
strange sort of auction because of the fact that there may be a soft "reserve price"
that is independent of the selling price. A simple example of how this could end
badly is where the bidder of the hypothetical pair wins the auction for 3 dollars.
The auctioned partner is so offended that, although they went on the date, there
was no happily ever after. The bidder, although actually having quite a high 
valuation of the auctioned partner might not have bid high because he understood
the probability was very low anybody else would win the auction when he bid anything
over 3 dollars. Clearly there is an incentive for the bidder to not only take into
account his own probability of winning in his consideration but also how the object
of the bid feels about the winning bid as well.

I will go into a bit of math a bit later... Needless to say this pair desperately
needs a strategy!

To begin thinking about this we should dive into two different kinds of auctions
that appear in many introductions on the topic. 

1. First Price Auction
2. Second Price Auction 

There are many many others and an infinite variation on these two alone but 
let's go into a tiny bit of detail. We will show soon how the dating auction, 
even when using a second price mechanism approaches a first price revenue.

# To Explain the Two Basic Auctions<a name="explanation1"></a>

A first price auction is your standard auction where there are a bunch of people
in a room screaming and the auctioneer listens for the highest bid(actually this
is an english auction but very similar) and at the end of the auction when the 
auctioneer decides the game has been played sells the item for the price that 
was shouted. 

A second price auction is also a standard auction but less widely known to 
lay-people. It is a variation where instead of paying the price that you shouted 
for the item, you pay the price of the second highest bidder's bid. 
You may ask "Why is this even a thing?" The answer to that when you pay the 
second highest bid it becomes in your favor to bid exactly how much you value the
item.

Let's do some math:

Let $ \beta_I(x) $ and $ \beta_{II}(x) $ be the strategy for a first and second
price bidder respectively where x is the value the bidder actually places on the
object. Let $ f(x) $ be the probability distribution function that the bidder 
places a value x on the object. 
<br/>

$$ F(x) = \int_0^x{f(y)dy} $$

<br/>
F(x) is also known as the cumulative distribution function. That is F(x) represents the statement
"What is the probability that a bidder places a value x or less on an item?" 
Another quantity of interest for second price auction would be $ F_2(x) $. 
This $ F_2(x) $ could be read as "What is the probability that the second highest
bidder has a value x or less?" 
We can write this as a function of F(x) by realizing that saying "What is the 
probability that the second highest bidder has a value x or less?" is the same
as saying "What is the probability that one bidder has a value higher than x
and the rest lower than x?"

$$ F_2(x) = (1-F(x))F(x)^{N-1} $$

The derivative of this is also useful and will come into play later(TODO:DO THIS DERIVATIVE ON PAPER):

$$\frac{\partial F_2(x)}{x}= -f(x)(F(x)^{N-1}+(1-F(x))(N-1)(F(x)^{N-2})+)$$

Each bidder will want to maximize his returns. His returns are simply the 
difference in how much the bidder pays and how much he percieves he receives. 

## First Price Auction Derivation <a name="firstprice"></a>

$$\mu_I(x,\text{win}) =  \begin{cases} 
                        x-\beta_I(x),& \text{if win}\\
                        0 & \text{otherwise}
                        \end{cases}$$

This is saying that if the bidder loses then nothing is lost. If he wins then he
gets the object but loses his bid.

This can be written as a sum: 

$$ \mu^I(x) = \mu_I(x,\text{True}) F_2(\beta_I^{-1}(b)) + \mu_I(x,\text{False})*\
(1-F_2(\beta_I^{-1}(b))) = (x-\beta_I(x)) F_2(\beta_I^{-1}(b)) $$

Now the optimal strategy for a bidder is the $\beta$ that maximizes $\mu$.

$$\beta_p(x) = \underset{\beta}{\text{argmax}}\, \mu(x) $$

This yields the differential equation:

$$ (x-\beta_I(x))(\frac{\partial F_2}{\beta_I^{-1}} \
\frac{\partial{\beta_I^{-1}}}{\partial{\beta_I}})  = F_2(\beta_I^{-1}(b))$$

Notice we assumed that the distributions of values of all bidders are sampled
from the same distribution F from all bidders. This allows us to make the observation
that $\beta^{-1}(b) = x$. Said another way, there is a one to one correspondence
between what the bidder values the item at and what the bidder wants to bid. 


We can therefore say that 

$$\frac{\partial{\beta^{-1}}}{\partial{\beta}} =  \
\frac{1}{\frac{\partial{\beta}}{\partial{\beta^{-1}}}} = \
\frac{1}{\frac{\partial{\beta}}{\partial{x}}(\beta^{-1}(b))}$$

Rewriting the differential equations above with this in mind we get:

$$ xf(x) = F_2(x)\beta_I'(x)+\beta_I(x) f_2(x) = \frac{d}{dx}(F_2(x)\beta_I(x))$$

integrating:

$$ \int_0^x{yf_2(y)dy} =F_2(x)\beta_I(x) $$

Written in a different way:

$$ \beta_I(x) = \int_0^x{y \frac{f_2(y)}{F_2(x)}dy}$$

The right hand side is the expectation of the second highest value given the 
highest value is x.

We write it out one last time:

$$\beta_I(x) = E[y|y\lt x] $$

Apparently the first price bidder should bid what he/she expects the second
highest value will be given it is below their value for the object. This makes
intuitive sense since, although the bidder may improve their chances of winning
the object if they bid higher than their value, their expected winnings become
negative. They also don't want to pay their value since if they know they can win
at a bid lower than their value they would get more of a reward.

## Second Price Auction Derivation <a name="secondprice"></a>

For second price the process is simpler. 

We have 

$$\mu_{II}(x,\text{win}) =  \begin{cases} 
                        x-\beta_{II}^-(x),& \text{if win}\\
                        0 & \text{otherwise}
                        \end{cases}$$

Where $\beta_{II}^-$ is the second highest bid. Rewriting $\mu_{II}$ just like 
for the first price auction.

$$\mu_{II}(x) = (x-\beta_{II}^-(b))F_2(\beta_{II}^{-1}(b)) $$

We again want

$$\underset{\beta}{\text{argmax}}\,\mu_{II}(x)$$

Now we don't need to do any calculations here because we can notice something 
interesting. In the right hand side of $\mu_{II}$ we see that there is only one value of $\beta_{II}(b)$ that actually arrives in our equation. The second highest 
bid. This is then set to be constant. Therefore the only thing that can be changed
is the $F_2$ which is monotonically increasing. Therefore, $\mu_{II}$ is maximized
when the bid is the same as the value. That is
$$\beta_{II}(x) = x $$

# Dating Auction Derivation <a name="datingauctionderivation"></a>
Now that we have examined the first and second price auction, we want to take a
look at the dating auction. How is this different?

# Dating Auction Characteristics <a name="datingauctioncharacteristics"></a>

# Dating Auction Simulation <a name="datingauctionsimulation"></a>

# Happily Ever After <a name="happilyeverafter"></a>