---
layout: post
---

# Table of Contents
1. [Introduction](#introduction)
    1. [Explanation of First and Second Price Auctions](#explanation1)

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

## To Explain the Two Basic Auctions<a name="explanation1"></a>

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

Let $ \beta^I(x) $ and $ \beta^{II}(x) $ be the strategy for a first and second
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
as saying "What is the probability that one bidder has a bidder higher than x
and the rest lower than x?"

$$ F_2(x) = (1-F(x))F(x)^{N-1} $$

Each bidder will want to maximize his returns. His returns are simply the difference
in how much the bidder pays and how much he percieves he receives. 

$$\mu(x) =  \begin{cases} 
                        x-\beta(x),& \text{if win}\\
                        0 & \text{otherwise}
                        \end{cases}$$

This is saying that if the bidder loses then nothing is lost. If he wins then he
gets the object but loses his bid.
