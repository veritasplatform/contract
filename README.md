# contract
watch the contract


# to count up all the votes we need to watch the contract events and see the votes , to do that we run this function : 

ethervote = web3.eth.contract(contractABI).at(contractAddress);
var logVotes = ethervote.LogVote({proposalHash: proposalHash}, {fromBlock: 1800000});
// Wait for the events to be loaded
logVotes.watch(function(error, result){
    if (!error) {            
        // Do something whenever the event happens
      receivedEvent(result);
    }
})


will start reading all blocks from number 1.8M (when the contract was uploaded) then execute the receivedEvent() function once for each event. So how work this function? 

Var voteMap = {};
Function receivedEvent(event) {
    // Get the current balance of a voter             
    var bal = Number(web3.fromWei(web3.eth.getBalance(event.args.addr), "finney"));
    voteMap[res.args.addr] = {balance: bal, support: event.args.pro}; 
}

you can see that the LogVote event comes with three argumenst, proposalHash, Pro and Addr:


(event LogVote(bytes32 indexed proposalHash, bool pro, address addr);


So what this function does is that it will use the function web3.eth.getBalance to check the current ether balance of the address that voted, Then the function will save the balance, One advantage of using a map instead of an array is that this will automatically overwrite any previous information about that same address, so if someone votes twice, only their last opinion will be kept.






