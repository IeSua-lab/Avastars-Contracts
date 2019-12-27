# Avastar Metadata Generator

View Source: [contracts/AvastarMetadata.sol](https://github.com/Dapp-Wizards/Avastars-Contracts/blob/master/contracts/AvastarMetadata.sol)

**AvastarMetadata** **↗ Extends: [AvastarBase](contracts/AvastarBase.md), [AvastarTypes](contracts/AvastarTypes.md), [AccessControl](contracts/AccessControl.md)**

Generate Avastar metadata from on-chain data.
Don't call this contract directly. It is used by `AvastarTeleporter` to generate
the human and machine readable metadata for a given Avastar token Id. Since this
functionality is not built into the `AvastarTeleporter` contract, it can be upgraded
in that contract by setting a new address for this contract.

## Constructor

Construct AvastarMetadata contract.

```solidity
constructor() public
```

## Contract Members
**Constants & Variables**

```solidity
// private members
contract IAvastarTeleporter private teleporterContract;
string private mediaUriBase;
string private viewUriBase;

// internal members
string internal tokenUriBase;

```

## **Events**

- [TokenUriBaseSet](#tokenuribaseset)
- [MediaUriBaseSet](#mediauribaseset)
- [ViewUriBaseSet](#viewuribaseset)

### TokenUriBaseSet

Event emitted when TokenURI base changes

```solidity
event TokenUriBaseSet(string tokenUriBase)
```

**Arguments**

| Name        | Type           | Description  |
| ------------- |------------- | -----|
| tokenUriBase | string | the base URI for tokenURI calls | 

### MediaUriBaseSet

Event emitted when the `mediaUriBase` is set.
Only emitted when the `mediaUriBase` is set after contract deployment.

```solidity
event MediaUriBaseSet(string mediaUriBase)
```

**Arguments**

| Name        | Type           | Description  |
| ------------- |------------- | -----|
| mediaUriBase | string | the new URI | 

### ViewUriBaseSet

Event emitted when the `viewUriBase` is set.
Only emitted when the `viewUriBase` is set after contract deployment.

```solidity
event ViewUriBaseSet(string viewUriBase)
```

**Arguments**

| Name        | Type           | Description  |
| ------------- |------------- | -----|
| viewUriBase | string | the new URI | 

## **Functions**

- [isAvastarMetadata](#isavastarmetadata)
- [setTokenUriBase](#settokenuribase)
- [setMediaUriBase](#setmediauribase)
- [setViewUriBase](#setviewuribase)
- [viewURI](#viewuri)
- [mediaURI](#mediauri)
- [tokenURI](#tokenuri)
- [getAvastarMetadata](#getavastarmetadata)
- [assembleTraitMetadata](#assembletraitmetadata)

### isAvastarMetadata

Acknowledge contract is `AvastarMetadata`

```solidity
function isAvastarMetadata()
external pure
returns (bool)
```

**Returns**

| Name        | Type           | Description  |
| ------------- |------------- | -----|
|  | bool | always true | 

### setTokenUriBase

Set the base URI for creating `tokenURI` for each Avastar.
Only invokable by system admin role, when contract is paused and not upgraded.
If successful, emits an `TokenUriBaseSet` event.

```solidity
function setTokenUriBase(string _tokenUriBase)
external nonpayable onlySysAdmin whenPaused whenNotUpgraded 
```

**Arguments**

| Name        | Type           | Description  |
| ------------- |------------- | -----|
| _tokenUriBase | string | base for the ERC721 tokenURI | 

### setMediaUriBase

Set the base URI for the image of each Avastar.
Only invokable by system admin role, when contract is paused and not upgraded.
If successful, emits an `MediaUriBaseSet` event.

```solidity
function setMediaUriBase(string _mediaUriBase)
external nonpayable onlySysAdmin whenPaused whenNotUpgraded 
```

**Arguments**

| Name        | Type           | Description  |
| ------------- |------------- | -----|
| _mediaUriBase | string | base for the mediaURI shown in metadata for each Avastar | 

### setViewUriBase

Set the base URI for the image of each Avastar.
Only invokable by system admin role, when contract is paused and not upgraded.
If successful, emits an `MediaUriBaseSet` event.

```solidity
function setViewUriBase(string _viewUriBase)
external nonpayable onlySysAdmin whenPaused whenNotUpgraded 
```

**Arguments**

| Name        | Type           | Description  |
| ------------- |------------- | -----|
| _viewUriBase | string | base URI for viewing an Avastar on the Avastars website | 

### viewURI

Get view URI for a given Avastar Token ID.

```solidity
function viewURI(uint256 _tokenId)
public view
returns (string uri)
```

**Arguments**

| Name        | Type           | Description  |
| ------------- |------------- | -----|
| _tokenId | uint256 | the Token ID of a previously minted Avastar Prime or Replicant | 

**Returns**

| Name        | Type           | Description  |
| ------------- |------------- | -----|
| uri | string | the off-chain URI to view the Avastar on the Avastars website | 

### mediaURI

Get media URI for a given Avastar Token ID.

```solidity
function mediaURI(uint256 _tokenId)
public view
returns (string uri)
```

**Arguments**

| Name        | Type           | Description  |
| ------------- |------------- | -----|
| _tokenId | uint256 | the Token ID of a previously minted Avastar Prime or Replicant | 

**Returns**

| Name        | Type           | Description  |
| ------------- |------------- | -----|
| uri | string | the off-chain URI to the Avastar image | 

### tokenURI

Get token URI for a given Avastar Token ID.

```solidity
function tokenURI(uint256 _tokenId)
public view
returns (string uri)
```

**Arguments**

| Name        | Type           | Description  |
| ------------- |------------- | -----|
| _tokenId | uint256 | the Token ID of a previously minted Avastar Prime or Replicant | 

**Returns**

| Name        | Type           | Description  |
| ------------- |------------- | -----|
| uri | string | the Avastar's off-chain JSON metadata URI | 

### getAvastarMetadata

Get human-readable metadata for a given Avastar by Token ID.

```solidity
function getAvastarMetadata(uint256 _tokenId)
external view
returns (string metadata)
```

**Arguments**

| Name        | Type           | Description  |
| ------------- |------------- | -----|
| _tokenId | uint256 | the token id of the given Avastar | 

**Returns**

| Name        | Type           | Description  |
| ------------- |------------- | -----|
| metadata | string | the Avastar's human-readable metadata | 

### assembleTraitMetadata

Assemble the human-readable metadata for a given Trait hash.
Used internally by

```solidity
function assembleTraitMetadata(enum AvastarTypes.Generation _generation, uint256 _traitHash)
internal view
returns (string metadata)
```

**Arguments**

| Name        | Type           | Description  |
| ------------- |------------- | -----|
| _generation | enum AvastarTypes.Generation | the generation the Avastar belongs to | 
| _traitHash | uint256 | the Avastar's trait hash | 

**Returns**

| Name        | Type           | Description  |
| ------------- |------------- | -----|
| metadata | string | metdata the JSON trait metadata for the Avastar | 
