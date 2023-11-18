# Solidity-bootcamp-3

### challenge(Task-3)
In the last lesson, we implemented the create function which creates a new proposal.

In your last challenge you added a title field to the proposal. In this task, you will update the create function that we created on the last lesson so that, it would

1. also take title as a parameter 
2. create the proposal accordingly 
3. submit your code when you are finished

Solution:

```sol
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.18;

contract ProposalContract {

    struct Proposal {
        string title; // Title of the proposal
        string description; // Description of the proposal
        uint256 approve; // Number of approve votes
        uint256 reject; // Number of reject votes
        uint256 pass; // Number of pass votes
        uint256 total_vote_to_end; // When the total votes in the proposal reaches this limit, proposal ends
        bool current_state; // This shows the current state of the proposal, meaning whether if passes of fails
        bool is_active; // This shows if others can vote to our contract
    }

    mapping(uint256 => Proposal) proposal_history; // Recordings of previous proposals
    Counter _counter;

    constructor() {
        _counter = Counter(0, "");
    }

    function create(string calldata _title, string calldata _description, uint256 _total_vote_to_end) external {
        _counter.increment();
        proposal_history[_counter.current()] = Proposal(_title, _description, 0, 0, 0, _total_vote_to_end, false, true);
    }

    // Existing Counter struct and related functions
    struct Counter {
        uint number;
        string description;

        function increment() internal {
            number++;
        }

        function current() internal view returns (uint) {
            return number;
        }
    }
}

```
