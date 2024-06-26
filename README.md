# Smart-Contract-Management2
# Description
Smart contract management overseeing the creation, deployment, maintenance, and execution of smart contracts on blockchain platforms here an overview of smart contract management ethereum and avalanche Both platforms provide robust environments for smart contract development, but the choice between them can depend on specific use case requirements such as transaction speed, cost, and desired ecosystem.
# Function Code
// SPDX-License-Identifier: UNLICENSED

pragma solidity ^0.8.9;

contract Assessment {

    address payable public owner;
    
    uint256 public balance;
     event Deposit(uint256 amount);
    event Withdraw(uint256 amount);

    constructor(uint initBalance) payable {
        owner = payable(msg.sender);
        balance = initBalance;
    }

    function getBalance() public view returns(uint256){
        return balance;
    }

    function deposit(uint256 _amount) public payable {
        uint _previousBalance = balance;

        require(msg.sender == owner, "You are not the owner of this account");

        balance += _amount;
        assert(balance == _previousBalance + _amount);
        emit Deposit(_amount);
    }
    error InsufficientBalance(uint256 balance, uint256 withdrawAmount);

    function withdraw(uint256 _withdrawAmount) public {
        require(msg.sender == owner, "You are not the owner of this account");
        uint _previousBalance = balance;
        if (balance < _withdrawAmount) {
            revert InsufficientBalance({
                balance: balance,
                withdrawAmount: _withdrawAmount
            });
        }
        balance -= _withdrawAmount;
        assert(balance == (_previousBalance - _withdrawAmount));
        emit Withdraw(_withdrawAmount);
    }
}
# Author 
Michaela Ariane B. Cabrera 8214136@ntc.edu.ph
