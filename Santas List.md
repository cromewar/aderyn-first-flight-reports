# Aderyn Analysis Report

This report was generated by [Aderyn](https://github.com/Cyfrin/aderyn), a static analysis tool built by [Cyfrin](https://cyfrin.io), a blockchain security company. This report is not a substitute for manual audit or security review. It should not be relied upon for any purpose other than to assist in the identification of potential security vulnerabilities.
# Table of Contents

- [Summary](#summary)
  - [Files Summary](#files-summary)
  - [Files Details](#files-details)
  - [Issue Summary](#issue-summary)
- [NC Issues](#nc-issues)
  - [NC-1: Functions not used internally could be marked external](#nc-1-functions-not-used-internally-could-be-marked-external)
  - [NC-2: Constants should be defined and used instead of literals](#nc-2-constants-should-be-defined-and-used-instead-of-literals)
  - [NC-3: Event is missing `indexed` fields](#nc-3-event-is-missing-indexed-fields)


# Summary

## Files Summary

| Key | Value |
| --- | --- |
| .sol Files | 3 |
| Total nSLOC | 115 |


## Files Details

| Filepath | nSLOC |
| --- | --- |
| src/SantaToken.sol | 22 |
| src/SantasList.sol | 89 |
| src/TokenUri.sol | 4 |
| **Total** | **115** |


## Issue Summary

| Category | No. of Issues |
| --- | --- |
| Critical | 0 |
| High | 0 |
| Medium | 0 |
| Low | 0 |
| NC | 3 |


# NC Issues

## NC-1: Functions not used internally could be marked external



- Found in src/SantasList.sol [Line: 187](src/SantasList.sol#L187)

	```solidity
	    function tokenURI(uint256 /* tokenId */ ) public pure override returns (string memory) {
	```



## NC-2: Constants should be defined and used instead of literals



- Found in src/SantaToken.sol [Line: 25](src/SantaToken.sol#L25)

	```solidity
	        _mint(to, 1e18);
	```

- Found in src/SantaToken.sol [Line: 32](src/SantaToken.sol#L32)

	```solidity
	        _burn(from, 1e18);
	```



## NC-3: Event is missing `indexed` fields

Index event fields make the field more quickly accessible to off-chain tools that parse events. However, note that each index field costs extra gas during emission, so it's not necessarily best to index the maximum allowed per event (three fields). Each event should use three indexed fields if there are three or more fields, and gas usage is not particularly of concern for the events in question. If there are fewer than three fields, all of the fields should be indexed.

- Found in src/SantasList.sol [Line: 93](src/SantasList.sol#L93)

	```solidity
	    event CheckedOnce(address person, Status status);
	```

- Found in src/SantasList.sol [Line: 94](src/SantasList.sol#L94)

	```solidity
	    event CheckedTwice(address person, Status status);
	```


