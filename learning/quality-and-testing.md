---
title: Quality and Testing
tags: learning
---
# Quality and Testing

## Wait! That's not tested

Tech talk by Heather Reid - https://heatherreiduff.com/

Cost of failure can be very high especially if you have low resources (poor family / university story).

The more things you build, the more resources you spend, the less you can risk failure. Especially if those things you built were not successful for you.

Slicing = placing smaller bets.

How much does a slice cost? £10,000 per week at her company. Very small when it's not your money, very big when it's your student loan.

Think about what 10k bet you would place if it was your money / decision.

- Feature One: Appointments.

3 teams, 5 months to first delivery, 14 months to beginning full roll-out.

Estimated £700,000 cost to get to full rollout. Will take 4 years to make a profit, approx.

- Feature Two: Spot Booking.

Reserve your favourite spot in the gym in advance.

Much shorter timeline - 0.5 months to first delivery, 3 months to start roll-out. Saw use much sooner. £160,000, 3 years to make a profit.

But crucially it's generated lots of interest from studios who want to move to this system.

Who cares?

- The customer
    - If their feedback goes ignored for years... they'll disengage.
- Management
    - Investors, money...
- Investors
    - Money
- Developers
    - You want to be valuable, receive praise, not get fired, get a raise, and not be a bottleneck!
    - And you probably don't want to fail.

Testing: "Facilitate continuous discovery of information about the product to helpf the team make informed decisions about risk, quality, and success."

Testing helps get information to stakeholders that they care about - you need to get the right information, framed in the right way, to the right people.

Sources of information:

- Reviews (especially 1 star lol)
- Interviews / research
- Requests to close accounts
- Team discussions about requirements
- Exploratory testing
- Automation suite results
- Production monitoring
- etc.

Thinking in bets: we will always have incomplete information so we need to live with that.

Gather information, assess risk with that info, need to do that as quickly and cheaply as possible.

"Not testing sets us up to fail" - does it? A tester doesn't have to have touched software before it ships, Heather asserts.

Minimum Viable Product (now a meaningless term) vs Minimum Shippable Risk. A bet leads to learning which might lead to a product. MSR provides value to _someone_ and will hopefully eventually provide value to the customer.

Ask questions like:

- Smallest thing we can ship?
- What are our success metrics?
- How do we assess the risk?

What problem are we trying to solve? Without answering this question it's hard to determine what's shippable / viable.

Example of viable vs shippable:

- Viable = interactive slot booking - e.g. RyanAir seat picker
- Shippable = people who want a slot know the gym like the back of their hand. Therefore you can just give people a list of numbers and let them pick. They don't need a fancy map layout.

First rough draft gave them a chance to collect feedback. "Why are you skipping slot selection?"

Clear success metrics allowed them to slice thinner, take less risk, and as a happy side-effect got rid of the In Test column.

They were also able to get good usage data. The team's mental model got better with this. They didn't have to continue speculating on what a more refined version of the feature would look like.

Wait! That's not tested...

Well, yeah. But the goal is to manage risk, not do some testing for the sake of it. Throughout the story they were gathering information, from many sources, not just opening the page on a range of their own devices and going through some UI journeys.

Monitoring in production - what's there, what's missing.

A good first slice might be a bit of extra monitoring in the area you're interested in to then decide what to do.

Tech debt: maybe the first slice is a refactor so we can actually make changes in an old codebase with less risk.

Time vs money: How much does it cost, how much is it worth, how long until we expect it to turn a profit.

Retros should focus on metrics that you actually care about, burn-down charts that perfectly predicted your release aren't as important as how the feature performed.

It's ok to fail, but make sure you actually learn something from it that you can take forward. And look at successes too! What is it about it that is doing well?
