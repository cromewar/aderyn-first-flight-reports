**THIS CHECKLIST IS NOT COMPLETE**. Use `--show-ignored-findings` to show all the results.
Summary
 - [arbitrary-send-eth](#arbitrary-send-eth) (1 results) (High)
 - [weak-prng](#weak-prng) (1 results) (High)
 - [divide-before-multiply](#divide-before-multiply) (2 results) (Medium)
 - [incorrect-equality](#incorrect-equality) (1 results) (Medium)
 - [reentrancy-no-eth](#reentrancy-no-eth) (1 results) (Medium)
 - [unused-return](#unused-return) (8 results) (Medium)
 - [missing-zero-check](#missing-zero-check) (2 results) (Low)
 - [reentrancy-events](#reentrancy-events) (2 results) (Low)
 - [timestamp](#timestamp) (1 results) (Low)
 - [assembly](#assembly) (4 results) (Informational)
 - [pragma](#pragma) (1 results) (Informational)
 - [dead-code](#dead-code) (1 results) (Informational)
 - [solc-version](#solc-version) (17 results) (Informational)
 - [low-level-calls](#low-level-calls) (6 results) (Informational)
 - [naming-convention](#naming-convention) (2 results) (Informational)
 - [redundant-statements](#redundant-statements) (1 results) (Informational)
 - [similar-names](#similar-names) (1 results) (Informational)
 - [cache-array-length](#cache-array-length) (3 results) (Optimization)
 - [constable-states](#constable-states) (3 results) (Optimization)
 - [immutable-states](#immutable-states) (1 results) (Optimization)
## arbitrary-send-eth
Impact: High
Confidence: Medium
 - [ ] ID-0
[PuppyRaffle.withdrawFees()](src/PuppyRaffle.sol#L157-L163) sends eth to arbitrary user
        Dangerous calls:
        - [(success) = feeAddress.call{value: feesToWithdraw}()](src/PuppyRaffle.sol#L161)

src/PuppyRaffle.sol#L157-L163


## weak-prng
Impact: High
Confidence: Medium
 - [ ] ID-1
[PuppyRaffle.selectWinner()](src/PuppyRaffle.sol#L125-L154) uses a weak PRNG: "[winnerIndex = uint256(keccak256(bytes)(abi.encodePacked(msg.sender,block.timestamp,block.difficulty))) % players.length](src/PuppyRaffle.sol#L128-L129)"

src/PuppyRaffle.sol#L125-L154


## divide-before-multiply
Impact: Medium
Confidence: Medium
 - [ ] ID-2
[Base64.decode(string)](lib/base64/base64.sol#L68-L129) performs a multiplication on the result of a division:
        - [decodedLen = (data.length / 4) * 3](lib/base64/base64.sol#L78)

lib/base64/base64.sol#L68-L129


 - [ ] ID-3
[Base64.encode(bytes)](lib/base64/base64.sol#L15-L66) performs a multiplication on the result of a division:
        - [encodedLen = 4 * ((data.length + 2) / 3)](lib/base64/base64.sol#L22)

lib/base64/base64.sol#L15-L66


## incorrect-equality
Impact: Medium
Confidence: High
 - [ ] ID-4
[PuppyRaffle.withdrawFees()](src/PuppyRaffle.sol#L157-L163) uses a dangerous strict equality:
        - [require(bool,string)(address(this).balance == uint256(totalFees),PuppyRaffle: There are currently players active!)](src/PuppyRaffle.sol#L158)

src/PuppyRaffle.sol#L157-L163


## reentrancy-no-eth
Impact: Medium
Confidence: Medium
 - [ ] ID-5
Reentrancy in [PuppyRaffle.refund(uint256)](src/PuppyRaffle.sol#L96-L105):
        External calls:
        - [address(msg.sender).sendValue(entranceFee)](src/PuppyRaffle.sol#L101)
        State variables written after the call(s):
        - [players[playerIndex] = address(0)](src/PuppyRaffle.sol#L103)
        [PuppyRaffle.players](src/PuppyRaffle.sol#L23) can be used in cross function reentrancies:
        - [PuppyRaffle.enterRaffle(address[])](src/PuppyRaffle.sol#L79-L92)
        - [PuppyRaffle.getActivePlayerIndex(address)](src/PuppyRaffle.sol#L110-L117)
        - [PuppyRaffle.players](src/PuppyRaffle.sol#L23)
        - [PuppyRaffle.refund(uint256)](src/PuppyRaffle.sol#L96-L105)
        - [PuppyRaffle.selectWinner()](src/PuppyRaffle.sol#L125-L154)

src/PuppyRaffle.sol#L96-L105


## unused-return
Impact: Medium
Confidence: Medium
 - [ ] ID-6
[ERC721._transfer(address,address,uint256)](lib/openzeppelin-contracts/contracts/token/ERC721/ERC721.sol#L387-L402) ignores return value by [_holderTokens[from].remove(tokenId)](lib/openzeppelin-contracts/contracts/token/ERC721/ERC721.sol#L396)

lib/openzeppelin-contracts/contracts/token/ERC721/ERC721.sol#L387-L402


 - [ ] ID-7
[ERC721._mint(address,uint256)](lib/openzeppelin-contracts/contracts/token/ERC721/ERC721.sol#L333-L344) ignores return value by [_holderTokens[to].add(tokenId)](lib/openzeppelin-contracts/contracts/token/ERC721/ERC721.sol#L339)

lib/openzeppelin-contracts/contracts/token/ERC721/ERC721.sol#L333-L344


 - [ ] ID-8
[ERC721._transfer(address,address,uint256)](lib/openzeppelin-contracts/contracts/token/ERC721/ERC721.sol#L387-L402) ignores return value by [_tokenOwners.set(tokenId,to)](lib/openzeppelin-contracts/contracts/token/ERC721/ERC721.sol#L399)

lib/openzeppelin-contracts/contracts/token/ERC721/ERC721.sol#L387-L402


 - [ ] ID-9
[ERC721._burn(uint256)](lib/openzeppelin-contracts/contracts/token/ERC721/ERC721.sol#L356-L374) ignores return value by [_tokenOwners.remove(tokenId)](lib/openzeppelin-contracts/contracts/token/ERC721/ERC721.sol#L371)

lib/openzeppelin-contracts/contracts/token/ERC721/ERC721.sol#L356-L374


 - [ ] ID-10
[ERC721._mint(address,uint256)](lib/openzeppelin-contracts/contracts/token/ERC721/ERC721.sol#L333-L344) ignores return value by [_tokenOwners.set(tokenId,to)](lib/openzeppelin-contracts/contracts/token/ERC721/ERC721.sol#L341)

lib/openzeppelin-contracts/contracts/token/ERC721/ERC721.sol#L333-L344


 - [ ] ID-11
[ERC721._burn(uint256)](lib/openzeppelin-contracts/contracts/token/ERC721/ERC721.sol#L356-L374) ignores return value by [_holderTokens[owner].remove(tokenId)](lib/openzeppelin-contracts/contracts/token/ERC721/ERC721.sol#L369)

lib/openzeppelin-contracts/contracts/token/ERC721/ERC721.sol#L356-L374


 - [ ] ID-12
[ERC721._transfer(address,address,uint256)](lib/openzeppelin-contracts/contracts/token/ERC721/ERC721.sol#L387-L402) ignores return value by [_holderTokens[to].add(tokenId)](lib/openzeppelin-contracts/contracts/token/ERC721/ERC721.sol#L397)

lib/openzeppelin-contracts/contracts/token/ERC721/ERC721.sol#L387-L402


 - [ ] ID-13
[ERC721.tokenByIndex(uint256)](lib/openzeppelin-contracts/contracts/token/ERC721/ERC721.sol#L180-L183) ignores return value by [(tokenId) = _tokenOwners.at(index)](lib/openzeppelin-contracts/contracts/token/ERC721/ERC721.sol#L181)

lib/openzeppelin-contracts/contracts/token/ERC721/ERC721.sol#L180-L183


## missing-zero-check
Impact: Low
Confidence: Medium
 - [ ] ID-14
[PuppyRaffle.changeFeeAddress(address).newFeeAddress](src/PuppyRaffle.sol#L167) lacks a zero-check on :
                - [feeAddress = newFeeAddress](src/PuppyRaffle.sol#L168)

src/PuppyRaffle.sol#L167


 - [ ] ID-15
[PuppyRaffle.constructor(uint256,address,uint256)._feeAddress](src/PuppyRaffle.sol#L60) lacks a zero-check on :
                - [feeAddress = _feeAddress](src/PuppyRaffle.sol#L62)

src/PuppyRaffle.sol#L60


## reentrancy-events
Impact: Low
Confidence: Medium
 - [ ] ID-16
Reentrancy in [PuppyRaffle.refund(uint256)](src/PuppyRaffle.sol#L96-L105):
        External calls:
        - [address(msg.sender).sendValue(entranceFee)](src/PuppyRaffle.sol#L101)
        Event emitted after the call(s):
        - [RaffleRefunded(playerAddress)](src/PuppyRaffle.sol#L104)

src/PuppyRaffle.sol#L96-L105


 - [ ] ID-17
Reentrancy in [PuppyRaffle.selectWinner()](src/PuppyRaffle.sol#L125-L154):
        External calls:
        - [(success) = winner.call{value: prizePool}()](src/PuppyRaffle.sol#L151)
        - [_safeMint(winner,tokenId)](src/PuppyRaffle.sol#L153)
                - [returndata = to.functionCall(abi.encodeWithSelector(IERC721Receiver(to).onERC721Received.selector,_msgSender(),from,tokenId,_data),ERC721: transfer to non ERC721Receiver implementer)](lib/openzeppelin-contracts/contracts/token/ERC721/ERC721.sol#L441-L447)
                - [(success,returndata) = target.call{value: value}(data)](lib/openzeppelin-contracts/contracts/utils/Address.sol#L119)
        External calls sending eth:
        - [(success) = winner.call{value: prizePool}()](src/PuppyRaffle.sol#L151)
        - [_safeMint(winner,tokenId)](src/PuppyRaffle.sol#L153)
                - [(success,returndata) = target.call{value: value}(data)](lib/openzeppelin-contracts/contracts/utils/Address.sol#L119)
        Event emitted after the call(s):
        - [Transfer(address(0),to,tokenId)](lib/openzeppelin-contracts/contracts/token/ERC721/ERC721.sol#L343)
                - [_safeMint(winner,tokenId)](src/PuppyRaffle.sol#L153)

src/PuppyRaffle.sol#L125-L154


## timestamp
Impact: Low
Confidence: Medium
 - [ ] ID-18
[PuppyRaffle.selectWinner()](src/PuppyRaffle.sol#L125-L154) uses timestamp for comparisons
        Dangerous comparisons:
        - [require(bool,string)(block.timestamp >= raffleStartTime + raffleDuration,PuppyRaffle: Raffle not over)](src/PuppyRaffle.sol#L126)

src/PuppyRaffle.sol#L125-L154


## assembly
Impact: Informational
Confidence: High
 - [ ] ID-19
[Address.isContract(address)](lib/openzeppelin-contracts/contracts/utils/Address.sol#L26-L35) uses assembly
        - [INLINE ASM](lib/openzeppelin-contracts/contracts/utils/Address.sol#L33)

lib/openzeppelin-contracts/contracts/utils/Address.sol#L26-L35


 - [ ] ID-20
[Address._verifyCallResult(bool,bytes,string)](lib/openzeppelin-contracts/contracts/utils/Address.sol#L171-L188) uses assembly
        - [INLINE ASM](lib/openzeppelin-contracts/contracts/utils/Address.sol#L180-L183)

lib/openzeppelin-contracts/contracts/utils/Address.sol#L171-L188


 - [ ] ID-21
[Base64.encode(bytes)](lib/base64/base64.sol#L15-L66) uses assembly
        - [INLINE ASM](lib/base64/base64.sol#L27-L63)

lib/base64/base64.sol#L15-L66


 - [ ] ID-22
[Base64.decode(string)](lib/base64/base64.sol#L68-L129) uses assembly
        - [INLINE ASM](lib/base64/base64.sol#L83-L126)

lib/base64/base64.sol#L68-L129


## pragma
Impact: Informational
Confidence: High
 - [ ] ID-23
Different versions of Solidity are used:
        - Version used: ['>=0.6.0', '>=0.6.0<0.8.0', '>=0.6.2<0.8.0', '^0.7.6']
        - [>=0.6.0](lib/base64/base64.sol#L3)
        - [>=0.6.0<0.8.0](lib/openzeppelin-contracts/contracts/access/Ownable.sol#L3)
        - [>=0.6.0<0.8.0](lib/openzeppelin-contracts/contracts/introspection/ERC165.sol#L3)
        - [>=0.6.0<0.8.0](lib/openzeppelin-contracts/contracts/introspection/IERC165.sol#L3)
        - [>=0.6.0<0.8.0](lib/openzeppelin-contracts/contracts/math/SafeMath.sol#L3)
        - [>=0.6.0<0.8.0](lib/openzeppelin-contracts/contracts/token/ERC721/ERC721.sol#L3)
        - [>=0.6.0<0.8.0](lib/openzeppelin-contracts/contracts/token/ERC721/IERC721Receiver.sol#L3)
        - [>=0.6.0<0.8.0](lib/openzeppelin-contracts/contracts/utils/Context.sol#L3)
        - [>=0.6.0<0.8.0](lib/openzeppelin-contracts/contracts/utils/EnumerableMap.sol#L3)
        - [>=0.6.0<0.8.0](lib/openzeppelin-contracts/contracts/utils/EnumerableSet.sol#L3)
        - [>=0.6.0<0.8.0](lib/openzeppelin-contracts/contracts/utils/Strings.sol#L3)
        - [>=0.6.2<0.8.0](lib/openzeppelin-contracts/contracts/token/ERC721/IERC721.sol#L3)
        - [>=0.6.2<0.8.0](lib/openzeppelin-contracts/contracts/token/ERC721/IERC721Enumerable.sol#L3)
        - [>=0.6.2<0.8.0](lib/openzeppelin-contracts/contracts/token/ERC721/IERC721Metadata.sol#L3)
        - [>=0.6.2<0.8.0](lib/openzeppelin-contracts/contracts/utils/Address.sol#L3)
        - [^0.7.6](src/PuppyRaffle.sol#L2)

lib/base64/base64.sol#L3


## dead-code
Impact: Informational
Confidence: Medium
 - [ ] ID-24
[PuppyRaffle._isActivePlayer()](src/PuppyRaffle.sol#L173-L180) is never used and should be removed

src/PuppyRaffle.sol#L173-L180


## solc-version
Impact: Informational
Confidence: High
 - [ ] ID-25
Pragma version[>=0.6.2<0.8.0](lib/openzeppelin-contracts/contracts/token/ERC721/IERC721.sol#L3) is too complex

lib/openzeppelin-contracts/contracts/token/ERC721/IERC721.sol#L3


 - [ ] ID-26
Pragma version[>=0.6.2<0.8.0](lib/openzeppelin-contracts/contracts/token/ERC721/IERC721Metadata.sol#L3) is too complex

lib/openzeppelin-contracts/contracts/token/ERC721/IERC721Metadata.sol#L3


 - [ ] ID-27
Pragma version[>=0.6.0<0.8.0](lib/openzeppelin-contracts/contracts/introspection/ERC165.sol#L3) is too complex

lib/openzeppelin-contracts/contracts/introspection/ERC165.sol#L3


 - [ ] ID-28
Pragma version[>=0.6.0<0.8.0](lib/openzeppelin-contracts/contracts/token/ERC721/ERC721.sol#L3) is too complex

lib/openzeppelin-contracts/contracts/token/ERC721/ERC721.sol#L3


 - [ ] ID-29
Pragma version[>=0.6.0<0.8.0](lib/openzeppelin-contracts/contracts/utils/EnumerableSet.sol#L3) is too complex

lib/openzeppelin-contracts/contracts/utils/EnumerableSet.sol#L3


 - [ ] ID-30
Pragma version[>=0.6.0<0.8.0](lib/openzeppelin-contracts/contracts/utils/Strings.sol#L3) is too complex

lib/openzeppelin-contracts/contracts/utils/Strings.sol#L3


 - [ ] ID-31
Pragma version[>=0.6.0<0.8.0](lib/openzeppelin-contracts/contracts/introspection/IERC165.sol#L3) is too complex

lib/openzeppelin-contracts/contracts/introspection/IERC165.sol#L3


 - [ ] ID-32
Pragma version[>=0.6.0<0.8.0](lib/openzeppelin-contracts/contracts/utils/Context.sol#L3) is too complex

lib/openzeppelin-contracts/contracts/utils/Context.sol#L3


 - [ ] ID-33
Pragma version[>=0.6.2<0.8.0](lib/openzeppelin-contracts/contracts/utils/Address.sol#L3) is too complex

lib/openzeppelin-contracts/contracts/utils/Address.sol#L3


 - [ ] ID-34
Pragma version[>=0.6.2<0.8.0](lib/openzeppelin-contracts/contracts/token/ERC721/IERC721Enumerable.sol#L3) is too complex

lib/openzeppelin-contracts/contracts/token/ERC721/IERC721Enumerable.sol#L3


 - [ ] ID-35
Pragma version[>=0.6.0<0.8.0](lib/openzeppelin-contracts/contracts/math/SafeMath.sol#L3) is too complex

lib/openzeppelin-contracts/contracts/math/SafeMath.sol#L3


 - [ ] ID-36
Pragma version[>=0.6.0<0.8.0](lib/openzeppelin-contracts/contracts/access/Ownable.sol#L3) is too complex

lib/openzeppelin-contracts/contracts/access/Ownable.sol#L3


 - [ ] ID-37
Pragma version[>=0.6.0<0.8.0](lib/openzeppelin-contracts/contracts/token/ERC721/IERC721Receiver.sol#L3) is too complex

lib/openzeppelin-contracts/contracts/token/ERC721/IERC721Receiver.sol#L3


 - [ ] ID-38
Pragma version[>=0.6.0](lib/base64/base64.sol#L3) allows old versions

lib/base64/base64.sol#L3


 - [ ] ID-39
solc-0.7.6 is not recommended for deployment

 - [ ] ID-40
Pragma version[>=0.6.0<0.8.0](lib/openzeppelin-contracts/contracts/utils/EnumerableMap.sol#L3) is too complex

lib/openzeppelin-contracts/contracts/utils/EnumerableMap.sol#L3


 - [ ] ID-41
Pragma version[^0.7.6](src/PuppyRaffle.sol#L2) allows old versions

src/PuppyRaffle.sol#L2


## low-level-calls
Impact: Informational
Confidence: High
 - [ ] ID-42
Low level call in [PuppyRaffle.selectWinner()](src/PuppyRaffle.sol#L125-L154):
        - [(success) = winner.call{value: prizePool}()](src/PuppyRaffle.sol#L151)

src/PuppyRaffle.sol#L125-L154


 - [ ] ID-43
Low level call in [Address.functionStaticCall(address,bytes,string)](lib/openzeppelin-contracts/contracts/utils/Address.sol#L139-L145):
        - [(success,returndata) = target.staticcall(data)](lib/openzeppelin-contracts/contracts/utils/Address.sol#L143)

lib/openzeppelin-contracts/contracts/utils/Address.sol#L139-L145


 - [ ] ID-44
Low level call in [Address.functionCallWithValue(address,bytes,uint256,string)](lib/openzeppelin-contracts/contracts/utils/Address.sol#L114-L121):
        - [(success,returndata) = target.call{value: value}(data)](lib/openzeppelin-contracts/contracts/utils/Address.sol#L119)

lib/openzeppelin-contracts/contracts/utils/Address.sol#L114-L121


 - [ ] ID-45
Low level call in [Address.sendValue(address,uint256)](lib/openzeppelin-contracts/contracts/utils/Address.sol#L53-L59):
        - [(success) = recipient.call{value: amount}()](lib/openzeppelin-contracts/contracts/utils/Address.sol#L57)

lib/openzeppelin-contracts/contracts/utils/Address.sol#L53-L59


 - [ ] ID-46
Low level call in [PuppyRaffle.withdrawFees()](src/PuppyRaffle.sol#L157-L163):
        - [(success) = feeAddress.call{value: feesToWithdraw}()](src/PuppyRaffle.sol#L161)

src/PuppyRaffle.sol#L157-L163


 - [ ] ID-47
Low level call in [Address.functionDelegateCall(address,bytes,string)](lib/openzeppelin-contracts/contracts/utils/Address.sol#L163-L169):
        - [(success,returndata) = target.delegatecall(data)](lib/openzeppelin-contracts/contracts/utils/Address.sol#L167)

lib/openzeppelin-contracts/contracts/utils/Address.sol#L163-L169


## naming-convention
Impact: Informational
Confidence: High
 - [ ] ID-48
Parameter [ERC721.safeTransferFrom(address,address,uint256,bytes)._data](lib/openzeppelin-contracts/contracts/token/ERC721/ERC721.sol#L245) is not in mixedCase

lib/openzeppelin-contracts/contracts/token/ERC721/ERC721.sol#L245


 - [ ] ID-49
Parameter [Base64.decode(string)._data](lib/base64/base64.sol#L68) is not in mixedCase

lib/base64/base64.sol#L68


## redundant-statements
Impact: Informational
Confidence: High
 - [ ] ID-50
Redundant expression "[this](lib/openzeppelin-contracts/contracts/utils/Context.sol#L21)" in[Context](lib/openzeppelin-contracts/contracts/utils/Context.sol#L15-L24)

lib/openzeppelin-contracts/contracts/utils/Context.sol#L21


## similar-names
Impact: Informational
Confidence: Medium
 - [ ] ID-51
Variable [Base64.TABLE_DECODE](lib/base64/base64.sol#L10-L13) is too similar to [Base64.TABLE_ENCODE](lib/base64/base64.sol#L9)

lib/base64/base64.sol#L10-L13


## cache-array-length
Impact: Optimization
Confidence: High
 - [ ] ID-52
Loop condition [i < players.length](src/PuppyRaffle.sol#L111) should use cached array length instead of referencing `length` member of the storage array.

src/PuppyRaffle.sol#L111


 - [ ] ID-53
Loop condition [i < players.length](src/PuppyRaffle.sol#L174) should use cached array length instead of referencing `length` member of the storage array.

src/PuppyRaffle.sol#L174


 - [ ] ID-54
Loop condition [j < players.length](src/PuppyRaffle.sol#L87) should use cached array length instead of referencing `length` member of the storage array.

src/PuppyRaffle.sol#L87


## constable-states
Impact: Optimization
Confidence: High
 - [ ] ID-55
[PuppyRaffle.commonImageUri](src/PuppyRaffle.sol#L38) should be constant

src/PuppyRaffle.sol#L38


 - [ ] ID-56
[PuppyRaffle.legendaryImageUri](src/PuppyRaffle.sol#L48) should be constant

src/PuppyRaffle.sol#L48


 - [ ] ID-57
[PuppyRaffle.rareImageUri](src/PuppyRaffle.sol#L43) should be constant

src/PuppyRaffle.sol#L43


## immutable-states
Impact: Optimization
Confidence: High
 - [ ] ID-58
[PuppyRaffle.raffleDuration](src/PuppyRaffle.sol#L24) should be immutable

src/PuppyRaffle.sol#L24