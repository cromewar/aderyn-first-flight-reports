# Aderyn Analysis Report

This report was generated by [Aderyn](https://github.com/Cyfrin/aderyn), a static analysis tool built by [Cyfrin](https://cyfrin.io), a blockchain security company. This report is not a substitute for manual audit or security review. It should not be relied upon for any purpose other than to assist in the identification of potential security vulnerabilities.
# Table of Contents

- [Summary](#summary)
  - [Files Summary](#files-summary)
  - [Files Details](#files-details)
  - [Issue Summary](#issue-summary)
- [Low Issues](#low-issues)
  - [L-1: Solidity pragma should be specific, not wide](#l-1-solidity-pragma-should-be-specific-not-wide)
  - [L-2: PUSH0 is not supported by all chains](#l-2-push0-is-not-supported-by-all-chains)


# Summary

## Files Summary

| Key | Value |
| --- | --- |
| .sol Files | 1 |
| Total nSLOC | 46 |


## Files Details

| Filepath | nSLOC |
| --- | --- |
| src/MathMasters.sol | 46 |
| **Total** | **46** |


## Issue Summary

| Category | No. of Issues |
| --- | --- |
| Critical | 0 |
| High | 0 |
| Medium | 0 |
| Low | 2 |
| NC | 0 |


# Low Issues

## L-1: Solidity pragma should be specific, not wide

Consider using a specific version of Solidity in your contracts instead of a wide version. For example, instead of `pragma solidity ^0.8.0;`, use `pragma solidity 0.8.0;`

- Found in src/MathMasters.sol [Line: 3](src/MathMasters.sol#L3)

	```solidity
	pragma solidity ^0.8.3;
	```



## L-2: PUSH0 is not supported by all chains

Solc compiler version 0.8.20 switches the default target EVM version to Shanghai, which means that the generated bytecode will include PUSH0 opcodes. Be sure to select the appropriate EVM version in case you intend to deploy on a chain other than mainnet like L2 chains that may not support PUSH0, otherwise deployment of your contracts will fail.

- Found in src/MathMasters.sol [Line: 3](src/MathMasters.sol#L3)

	```solidity
	pragma solidity ^0.8.3;
	```


