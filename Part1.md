# Blockchain Consensuses Comparison - Part 1: Ouroboros| Casper| Toda| Algorand

## Motivation
Each month at least one new consensus (consensus protocols) is being introduced to community. There are a lot of reviews and analyses, but all of them do use not one methodology. It is difficult to compare consensuses without structured approach. I am proposing my vision (and of course comparison) how to analyze different consensuses.

## Criteria
I have tried to combine the most important aspects. Of course this list could be extended, but will cause difficulty in information perception.

### Generic characteristics
- What is **kind** of protocol?
- What is **maturity** of protocol?

### Main questions
1. **Who** should **produce** the next block of updates to apply to the database?
2. **When** should **the next block** be produced?
3. **What transactions** should be included in the block?
4. How are **changes to the protocol** applied?
5. How should **competing transaction** histories be resolved?
6. How should blockchain **forks be resolved**?

### Additional metrics
- Are **smart contracts** supported?
- How is **side-chains inter-operating** implemented?
- How is **performance** changing on growing number of nodes?
- What is **limit of nodes** in consensus?
- What is **block** producing **interval**?
- What is period of **irreversibility** (99.99%, 10% Adversary)?
- How much is **transaction fee**?

### Resistance
- **Nothing-at-Stake**
- - incentives for nodes to vote on the correct block
- **Failure**
- - ability to reach consensus
- **Sybil** attacks
- - a single adversary is controlling multiple nodes on a network

## Summary table
Сombining all criteria into table and use color for cell background (protocol does not have information for) can help to see the drawbacks of consensuses.

|Criteria|Cardano|Casper FFG|Toda|Algorand|
|---|---|---|---|---|
|What is **kind** of protocol?|Delegation scheme on top of PoS|PoS overlay on top of PoW (Ethereum)|PoAW (Proof of Actual Work)|Scaling Byzantine Agreements|
|What is **maturity** of protocol?|Proposal|R&D|Expected to be released|Recommendations, Peer reviewed|R&D|
|**Who** should **produce** the next block of updates to apply to the database?|||||
|**When** should **the next block** be produced?|||||
|**What transactions** should be included in the block?|||||
|How are **changes to the protocol** applied?|||||
|How should **competing transaction** histories be resolved?|||||
|How should blockchain **forks be resolved**?|||||
|Are **smart contracts** supported?|||||
|How is **side-chains inter-operating** implemented?|||||
|How is **performance** changing on growing number of nodes?|||||
|What is **limit of nodes** in consensus?|||||
|What is **block** producing **interval**?|||||
|What is period of **irreversibility** (99.99%, 10% Adversary)?|||||
|How much is **transaction fee**?|||||
|**Nothing-at-Stake** resistance|||||
|**Failure** resistance|||||
|**Sybil** attacks resistance|||||