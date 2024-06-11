# MyToken

## Overview

MyToken is a simple smart contract written in Solidity for managing a custom ERC20-like token. The contract includes functionalities for minting and burning tokens, and keeps track of token balances for different addresses.

## Token Details

- **Token Name**: META
- **Token Abbreviation**: MTA
- **Total Supply**: Dynamic, managed through minting and burning

## Requirements

1. Public variables to store details about the token (Token Name, Token Abbreviation, Total Supply).
2. A mapping of addresses to their respective token balances.
3. A mint function to increase the total supply and the balance of a specified address.
4. A burn function to decrease the total supply and the balance of a specified address, with checks to ensure the address has sufficient balance.

## Functions

### `mint`

The `mint` function allows you to create new tokens and assign them to an address. It takes two parameters:
- `_address`: The address to which the minted tokens will be assigned.
- `_value`: The number of tokens to mint.

### `burn`

The `burn` function allows you to destroy tokens from an address. It takes two parameters:
- `_address`: The address from which the tokens will be burned.
- `_value`: The number of tokens to burn.

The function includes a check to ensure that the balance of the address is greater than or equal to the number of tokens to be burned.

## TEST_Code

```solidity
// SPDX-License-Identifier: MIT
pragma solidity 0.8.18;

/*
       REQUIREMENTS
    1. Your contract will have public variables that store the details about your coin (Token Name, Token Abbrv., Total Supply)
    2. Your contract will have a mapping of addresses to balances (address => uint)
    3. You will have a mint function that takes two parameters: an address and a value. 
       The function then increases the total supply by that number and increases the balance 
       of the “sender” address by that amount
    4. Your contract will have a burn function, which works the opposite of the mint function, as it will destroy tokens. 
       It will take an address and value just like the mint functions. It will then deduct the value from the total supply 
       and from the balance of the “sender”.
    5. Lastly, your burn function should have conditionals to make sure the balance of "sender" is greater than or equal 
       to the amount that is supposed to be burned.
*/

contract MyToken {
    // public variables here
    string public tokenName = "META";
    string public tokenAbbrv = "MTA";
    uint public totalSupply = 0;

    // mapping variable here
    mapping(address => uint) public balances;

    // mint function
    function mint(address _address, uint _value) public {
        totalSupply += _value;
        balances[_address] += _value;
    }

    // burn function
    function burn(address _address, uint _value) public {
        if (balances[_address] >= _value) {
            totalSupply -= _value;
            balances[_address] -= _value;
        }
    }
}
