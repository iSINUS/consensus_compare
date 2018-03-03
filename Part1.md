# Blockchain Consensuses Comparison - Part 1: Ouroboros, Casper, Toda, Algorand

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
    - incentives for nodes to vote on the correct block
- **Failure**
    - ability to reach consensus
- **Sybil** attacks
    - a single adversary is controlling multiple nodes on a network

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
|**Sybil** attacks resistance||{class="notdefined"}|||

<table>
    <thead>
        <tr>
            <th>Criteria</th>
            <th>Ouroboros</th>
            <th>Casper FFG</th>
            <th>Toda</th>
            <th>Algorand</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>What is
                <b>kind</b> of protocol?</td>
            <td>Delegation scheme on top of PoS</td>
            <td>PoS overlay on top of PoW (Ethereum)</td>
            <td>PoAW (Proof of Actual Work)</td>
            <td>Scaling Byzantine Agreements</td>
        </tr>
        <tr>
            <td>What is
                <b>maturity</b> of protocol?</td>
            <td>Proposal</td>
            <td>R&D</td>
            <td>Expected to be released</td>
            <td>Recommendations, Peer reviewed</td>
        </tr>
        <tr>
            <td>
                <b>Who</b> should
                <b>produce</b> the next block of updates to apply to the database?</td>
            <td>- Protocol relies on the assumption that nodes in the system have access to the current time
                <br> - Cardano SL uses Follow the Satoshi (FTS) algorithm to choose slot leaders (shared seed using XOR)
                <br> -- COMMITMENTS, OPENINGS, SHARES SENDING: time of sending is randomized within a small interval
                <br> - A number of shares for each stakeholder proportional to their stake.
                <br> - The same stakeholder can be chosen as a leader for multiple slots within an epoch
                <br> - Stake Delegation - delegation-by-proxy, heavyweight (in chain, stake threshold) and lightweight </td>
            <td>                - Casper’s logic lives inside an Ethereum smart contract
                <br> - To become a validator in Casper, one must hold ether (ETH) and deposit some ETH to be leveraged as stake into the Casper smart contract
                <br> - The "size“ of a validator in the active validator pool refers to the amount of ether that they deposited
                <br> - The block proposal mechanism - Nakamoto PoW (miners create the blocks)
                <br> -- In order to finalize blocks Casper’s PoS overlay takes control and has its validators vote on blocks trailing the PoW miners
             </td>
            <td>- The Merkle root of last block is used as a beacon in existing block to generate pseudo-randomness that is deterministic and universal
                <br> - Utilizing the beacon in a function to pseudorandomly select the Machines/managers of those TodaNotes (Group A) along with the Merkle root prior (Group B). Total of 64 managers (Group A + Group B) ​can work on building the Merkle proof
                <br> - If a manager from Group A does not have Merkle proof in subsequent block when it moves to Group B
                </td>
            <td>- Loosely synchronized clocks across all users
                <br> - Each step begins with cryptographic sortition (verifiable random functions (VRFs)), where all users check whether they have been selected as members in that step (unforgeable proof that she has been selected)
                <br> - Every user selected for block proposal also computes a proposed seed for next round
                <br> - A user is randomly selected, according to her total amount of money in the system, to propose a block
                <br> - A small committee of users, the verifiers, are similarly selected, and reach Byzantine Agreement on the block proposed by the first user
                </td>
        </tr>
        <tr>
            <td>
                <b>When</b> should
                <b>the next block</b> be produced?</td>
            <td>- The Ouroboros protocol divides the physical time into epochs, and each epoch is divided into slots
                <br> - Block should be produced within slot by slot leader
                <br> - One or more slots can remain empty (without generated blocks
                <br> - The majority of blocks (at least 50% + 1) must be (there is no control) generated during an epoch
                </td>
            <td> - The purpose of the consensus process is to "finalize" key blocks called "checkpoints“
                <br> - Every 100th block is a checkpoint
                <br> - There are epochs of some specified length (currently, 50 blocks) during which validators "vote" on the chain that they believe to be the canonical one
                <br> -- When two consecutive epochs achieve >2/3 votes-by-weight, the first epoch of these epochs is "finalized"
                <br> - ⅔ Vote Block_1 → Justify Block_1 → ⅔ Vote Block_2 → Finalize Block_1 (Block_2 is direct child of Block_1)
                </td>
            <td> - Race of producers and verifiers
                <br> - The first to deliver to the new TodaNote owner the Merkle proof
                </td>
            <td>- Two phases:
                <br> -- Block proposals are prioritized based on the proposing user’s priority, and users wait for a certain amount of time to receive the block
                <br> -- Committee members then broadcast a message which includes their proof of selection and vote
                <br> - Steps are not synchronized across users; each user checks for selection as soon as he observes the previous step had ended
                <br> - Gossips two kinds of messages: one contains just the priorities and proofs of the chosen block proposers (about 200 Bytes), and the other contains the entire block, which also includes the proposer’s sortition hash, and proof.
                </td>
        </tr>
        <tr>
            <td>
                <b>What transactions</b> should be included in the block?</td>
            <td> - Verified transactions
                <br> -- All unspent outputs called utxo, and this is a part of the special key-value database called Global State - node verify inputs agains it.
                <br> -- Legitime transactions have proof (witness).  Two corresponding versions of the witness: based on public key and based on script.
                <br> -- Transactions and proofs are stored in two separate places in a block - "segregated witness"
                </td>
            <td>- Ethereum rules
                    <br> - Based on transaction fee and gas limit - deciding by miner
                    </td>
            <td>- Testified transactions
                    <br> -- the check for authenticity of ownership proofs
                    <br> -- signatures
                    <br> -  Given that transaction must be a minimum of 17 TodaNote
                    <br> - No defined what exactly transactions
                    </td>
            <td>- Each user collects a block of pending transactions that they hear about, in case they are chosen to propose the next block
                    <br> - Sequence of transaction not defined (as received)
                    </td>
        </tr>
        <tr>
            <td>How are
                <b>changes to the protocol</b> applied?</td>
            <td>- On-chain voting and on-chain result fixing (of protocol updates)
                    <br> - There is no central entity responsible for maintaining or distributing updates, any such update is proposed under implicit or explicit agreement
                    <br> -- Explicit agreement: it has positive votes from majority of total stake
                    <br> -- Implicit agreement: it has positive votes from more stake than negative votes ⁠⁠⁠and⁠⁠⁠ it has been in blockchain for at least U slots.
                    <br> - The software updates is done automatically (Bittorrent-like solution to distribute updates), and updates are announced directly via the blockchain
                    <br> - Single official client at the begging, but a different client developed later
                    </td>
            <td>- Allows validators to pick their fault tolerance (built in client) thresholds while the network maintains the low overhead of Proof-of-Work.
                    <br> - The Ethereum Improvement Proposal
                    <br> -- More strict modified fork-choice rule should be followed by all users, validators, and even the underlying block proposal mechanism
                    </td>
            <td class="notdefined">- NOT DEFINED
                </td>
            <td class="notdefined">- NOT DEFINED
                </td>
        </tr>
        <tr>
            <td>How should
                <b>competing transaction</b> histories be resolved?</td>
            <td>- Time sequence (not directly explained)
                </td>
            <td>- Ethereum rules
                    <br> - Valid transactions can be moved from uncle to the next block
                    </td>
            <td class="notdefined">- NOT DEFINED
                </td>
            <td class="notdefined">- NO DEFINED
                    <br> - All decisions are through BA⋆ on proposed block
                    <br> -- reduces the problem to two options
                    <br> -- reaches agreement on proposed block, or agreeing on an empty block.
                    /td>
        </tr>
        <tr>
            <td>How should blockchain
                <b>forks be resolved</b>?</td>
            <td>- Genesis blocks are generated by each node internally (independently) between epochs – not stored
                    <br> - Each other node (not slot leader) accept only one of concurrent blocks
                    <br> - Takes the longest chain as a main
                    </td>
            <td>- Once a block is finalized "one can never go back“
                    <br> -- even if 99% of miners start supporting it
                    <br> - Rollback to checkpoint in case of fork
                    <br> - There are "slashing conditions" in smart contract
                    <br> -- If two incompatible blocks are finalized - validators did this are been sent into the Casper contract (block with evidence mined)
                    <br> -- The validator's entire deposit will be destroyed (except 4%, which is given to the evidence submitter as a "finder's fee")
                    <br> -- At least ⅓ of the total security deposits staked will be slashed
                    </td>
            <td>- NO FORKS
                </td>
            <td>- Periodically (once an hour) proposes a fork that all users should agree on
                    <br> - Uses BA⋆ to reach consensus on whether all users should, indeed, switch to this fork
                    </td>
        </tr>
        <tr>
            <td>Are
                <b>smart contracts</b> supported?</td>
            <td></td>
            <td></td>
            <td></td>
            <td></td>
        </tr>
        <tr>
            <td>How is
                <b>side-chains inter-operating</b> implemented?</td>
            <td></td>
            <td></td>
            <td></td>
            <td></td>
        </tr>
        <tr>
            <td>How is
                <b>performance</b> changing on growing number of nodes?</td>
            <td></td>
            <td></td>
            <td></td>
            <td></td>
        </tr>
        <tr>
            <td>What is
                <b>limit of nodes</b> in consensus?</td>
            <td></td>
            <td></td>
            <td></td>
            <td></td>
        </tr>
        <tr>
            <td>What is
                <b>block</b> producing
                <b>interval</b>?</td>
            <td></td>
            <td></td>
            <td></td>
            <td></td>
        </tr>
        <tr>
            <td>What is period of
                <b>irreversibility</b> (99.99%, 10% Adversary)?</td>
            <td></td>
            <td></td>
            <td></td>
            <td></td>
        </tr>
        <tr>
            <td>How much is
                <b>transaction fee</b>?</td>
            <td></td>
            <td></td>
            <td></td>
            <td></td>
        </tr>
        <tr>
            <td>
                <b>Nothing-at-Stake</b> resistance</td>
            <td></td>
            <td></td>
            <td></td>
            <td></td>
        </tr>
        <tr>
            <td>
                <b>Failure</b> resistance</td>
            <td></td>
            <td></td>
            <td></td>
            <td></td>
        </tr>
        <tr>
            <td>
                <b>Sybil</b> attacks resistance</td>
            <td></td>
            <td></td>
            <td></td>
            <td></td>
        </tr>
    </tbody>
</table>

<style>
    td {vertical-align: top}
    td.notdefined {
        background-color: rgba(255, 0, 0, 0.356);
        
    }
</style>
