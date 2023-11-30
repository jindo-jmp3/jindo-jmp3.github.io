# Auto-trader Project

## Overview 
We have 113K college basketball bets that represent all bets from a single agency under a larger entity from last college basketball season.
The *objective* is to produce new odds after each bet that is more accurate than the consensus provided.

### Parameters
Models built for college basketball main markets, specifically:
  - Full Game, 1st Half, 2nd Half for
  - Handicap, Moneyline, Game Total
  = 9 models in total

Models should be implemented in R or Python and they improve vs consensus odds in 3 metrics
  - Brier
  - AUROC
  - "profitability test", or a test where for each data point, each model goes into a contract with unit-size scaled by difference in perceived odds / value; we can discuss the exact implementation in more detail

If no such model(s) exist for a given market type, then that discovery is meaningful in itself.

A couple of additional requirements:
  1. parsimony over complexity
    . we value model simplicity, so a champion model should be built that is (relatively) basic, assuming it can beat the consensus
    . to use any model over that level of sophistication will require beating that model
  2. weekly check-ins
    . this could be either a call or email
    . the key is to keep everyone informed and up-to-date at a reasonable pace
  3. eye on implementation & initial strategy
    . if model(s) are found, then the idea would be to deploy this in a "test" environment fairly quickly
    . it's important to have an opinion of where, when, and how this could be deployed successfully


## Data Description
The dataset has 113,460 rows. These are bets occurred between Feb 2022 and Apr 2023, up to the end of March Madness Tourney. Each bet has a timestamp and associated game and market; they are all pre-match bets. Numerous features were joined on this dataset for predictive model purposes, including:
  - descriptors of the bet, like risk, win, line and odds
  - performance metrics for that player up to that day
  - information around a market consensus, which is effectively an average calculation based on 3 of sharp U.S. sportsbooks

Additional features may be necessary to get lift, such as
  - risk of the agency carried on that side / market up to that point
  - whether the bet is a "max" bet or not; we have a way of doing this efficiently without knowing precisely the given limits
  - player tendencies associated with the side or team

No data around the college basketball itself can be used.

You will also need to build your own target. The obvious choice is whether or not the wager is graded a win or loss, tossing out pushes. There are a deluve of modifications to that choice, however, and we will not make it a requirement to model using a specific target.
