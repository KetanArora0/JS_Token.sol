# JS_Token.sol
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.18;

contract MyToken {

    string public TokenName = "MetaCrafters";
    string public TokenAbbrv = "MTCR";
    uint public TotalSupply = 0;

    mapping (address => uint) public Balances;

    constructor() {
        // Initialize the contract owner's balance
        Balances[msg.sender] = 0;
    }

    function mint(address _address, uint _value) public {
        require(msg.sender == _address, "Only the owner of the address can mint tokens");
        TotalSupply += _value;
        Balances[_address] += _value;
    }

    function burn(address _address, uint _value) public {
        require(msg.sender == _address, "Only the owner of the address can burn tokens");
        require(Balances[_address] >= _value, "Insufficient balance");
        TotalSupply -= _value;
        Balances[_address] -= _value;
    }
}
