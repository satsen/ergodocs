# EIP-0021: Genuine Token Verification

## Description 

This EIP lists the common tokens of value with their unique identifier, so users as well as wallet and explorer applications can verify if a token is genuine. The EIP is meant to be updated regularly when new tokens of value are added.

## Motivation 

Ergo tokens can hold a certain value, best-known examples are the SigUSD and SigRSV tokens in use by the SigmaUSD stablecoin protocol. 
Tokens can be minted by every user, with a name and description free to choose. This means everyone can mint new tokens named "SigUSD", which bears a problem for end-users to decide if a token they received is genuine or not.

## Ergo tokens background

[See EIP-4](eip4.md): Ergo supports custom tokens as first-class citizens. A transaction can create out-of-thin-air tokens in its outputs if the token 
identifier is equal to the identifier of the first input box of the transaction.
As the box identifier is cryptographically unique, there's no chance to have the second token with the same identifier while the hash function being used 
is collision-resistant. 

In order to verify the authenticity of a token, the unique identifier of a token is needed to check.

## Process to add tokens to this list
As outlined before, this list should only hold tokens of value. This means that mainly tokens of financial value can be added. Before opening a PR to add your token to this list, ask yourself if your token is interesting for scammers. When the answer is no, the token should probably not added to this list. 
On rare occasions, tokens of a certain intrinsic value to the community could be added as well when there was a community vote with significant community participation.

## Recommended approach for applications showing tokens to end-users

### Verified tokens 
Applications should add a verification sign next to a token which is listed in the following [genuine tokens list](#genuine-tokens).

Proposed verification sign: [Material icons verified](https://fonts.google.com/icons?selected=Material%20Icons%20Outlined%3Averified%3A)

### Suspicious tokens
In order to protect end-users for confusion, it is decided for some tokens in the [genuine tokens list](#genuine-tokens) that the verbose name should be 
unique and should not be used by other tokens. 
This is not enforced by Ergo protocol, so applications should check if a token uses a unique name from the list and add a warning sign when needed.

Proposed warning sign: [Material icons report](https://fonts.google.com/icons?selected=Material%20Icons%20Outlined%3Areport%3A)

### Blocked tokens
Applications should show a warning sign next to tokens identified to be harmful or impersonating other tokens.

Proposed warning sign: [Material icons dangerous](https://fonts.google.com/icons?selected=Material%20Icons%20Outlined%3Adangerous%3A)

## Token lists

### Genuine tokens

| Verbose name       | Token id                                                         | Unique name | Issuer
| ------------------ |:----------------------------------------------------------------:| -----------:| ------
| SigUSD             | 03faf2cb329f2e90d6d23b58d91bbb6c046aa143261cc21f52fbe2824bfcbf04 | yes         | sigmausd.io
| SigRSV             | 003bd19d0187117f130b62e1bcab0939929ff5c7709f843c5c4dd158949285d0 | yes         | sigmausd.io

### Blocked tokens

| Token id                                        | 
|:-----------------------------------------------:| 
