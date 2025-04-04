<div align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/VIALabs-io/.github/main/profile/logo-white.svg" width="400">
    <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/VIALabs-io/.github/main/profile/logo-black.svg" width="400">
    <img src="https://raw.githubusercontent.com/VIALabs-io/.github/main/profile/logo-black.svg" alt="VIA Labs" width="400">
  </picture>
  
  <h1>
    <svg width="30" height="30" viewBox="0 0 30 30" xmlns="http://www.w3.org/2000/svg" style="vertical-align: middle;">
      <text x="0" y="25" font-family="Arial, sans-serif" font-size="25" font-weight="bold" fill="#FF00FF">//</text>
    </svg>
    CROSS-CHAIN COMMUNICATION
  </h1>
  
  <p>
    <a href="https://github.com/VIALabs-io"><img src="https://img.shields.io/badge/130+-NETWORKS-00E5E5?style=for-the-badge" alt="130+ Networks"></a>
    <a href="https://www.npmjs.com/package/@vialabs-io/contracts"><img src="https://img.shields.io/npm/v/@vialabs-io/npm-contracts?style=for-the-badge&color=FF00FF&label=NPM" alt="NPM Version"></a>
    <a href="https://discord.gg/vialabs"><img src="https://img.shields.io/badge/Discord-Join-00E5E5?style=for-the-badge&logo=discord&logoColor=white" alt="Discord"></a>
  </p>
  
  <h3>The future of Web3 is 
    <svg width="70" height="25" viewBox="0 0 70 25" xmlns="http://www.w3.org/2000/svg" style="vertical-align: middle;">
      <text x="0" y="18" font-family="Arial, sans-serif" font-size="18" font-weight="bold" fill="#00E5E5">unified</text>
    </svg> and 
    <svg width="90" height="25" viewBox="0 0 90 25" xmlns="http://www.w3.org/2000/svg" style="vertical-align: middle;">
      <text x="0" y="18" font-family="Arial, sans-serif" font-size="18" font-weight="bold" fill="#FF00FF">borderless</text>
    </svg>
  </h3>
  <h3>We enable true 
    <svg width="110" height="25" viewBox="0 0 110 25" xmlns="http://www.w3.org/2000/svg" style="vertical-align: middle;">
      <text x="0" y="18" font-family="Arial, sans-serif" font-size="18" font-weight="bold" fill="#FF00FF">cross-chain</text>
    </svg> 
    <svg width="90" height="25" viewBox="0 0 90 25" xmlns="http://www.w3.org/2000/svg" style="vertical-align: middle;">
      <text x="0" y="18" font-family="Arial, sans-serif" font-size="18" font-weight="bold" fill="#00E5E5">innovation</text>
    </svg> and private 
    <svg width="80" height="25" viewBox="0 0 80 25" xmlns="http://www.w3.org/2000/svg" style="vertical-align: middle;">
      <text x="0" y="18" font-family="Arial, sans-serif" font-size="18" font-weight="bold" fill="#00E5E5">off-chain</text>
    </svg> to 
    <svg width="80" height="25" viewBox="0 0 80 25" xmlns="http://www.w3.org/2000/svg" style="vertical-align: middle;">
      <text x="0" y="18" font-family="Arial, sans-serif" font-size="18" font-weight="bold" fill="#FF00FF">on-chain</text>
    </svg> connectivity
  </h3>
</div>

<br>

**VIA Protocol** allows developers to build applications that seamlessly operate across multiple blockchains and access private off chain data providing a unified experience for users regardless of their network from web2 to web3, large or small, public or private.

<br>


### <svg width="25" height="25" viewBox="0 0 25 25" xmlns="http://www.w3.org/2000/svg" style="vertical-align: middle;">
  <text x="0" y="18" font-family="Arial, sans-serif" font-size="18" font-weight="bold" fill="#00E5E5">//</text>
</svg> Cross-Chain Native Tokens

<div style="border-left: 3px solid #00E5E5; padding-left: 15px;">

Move custom tokens between chains without wrapping or bridges. One contract, multiple chains, native representation.

```solidity
// Bridge tokens to another chain
function bridge(uint _destChainId, address _recipient, uint _amount) external {
    _burn(msg.sender, _amount);
    _sendMessage(_destChainId, abi.encode(_recipient, _amount));
    emit TokensBridged(msg.sender, _destChainId, _recipient, _amount);
}

// Process incoming tokens from another chain
function _processMessage(uint _sourceChainId, uint, bytes calldata _data) internal override {
    (address _recipient, uint _amount) = abi.decode(_data, (address, uint));
    _mint(_recipient, _amount);
    emit TokensReceived(_sourceChainId, _recipient, _amount);
}
```
</div>

### <svg width="25" height="25" viewBox="0 0 25 25" xmlns="http://www.w3.org/2000/svg" style="vertical-align: middle;">
  <text x="0" y="18" font-family="Arial, sans-serif" font-size="18" font-weight="bold" fill="#FF00FF">//</text>
</svg> Cross-Chain NFTs

<div style="border-left: 3px solid #FF00FF; padding-left: 15px;">

Seamless NFT transfers with metadata between networks. Preserve provenance and history across blockchain ecosystems.

```solidity
// Bridge NFT to another chain
function bridge(uint _destChainId, address _recipient, uint _nftId) external {
    // Store metadata before burning
    NFTMetadata memory metadata = _tokenMetadata[_nftId];
    _burn(_nftId);
    _sendMessage(_destChainId, abi.encode(_recipient, _nftId, metadata));
    emit NFTBridged(msg.sender, _nftId, _destChainId, _recipient);
}

// Process incoming NFT from another chain
function _processMessage(uint _sourceChainId, uint, bytes calldata _data) internal override {
    (address _recipient, uint _nftId, NFTMetadata memory metadata) = 
        abi.decode(_data, (address, uint, NFTMetadata));
    
    // Mint the NFT on this chain with original metadata
    _mint(_recipient, _nftId);
    _tokenMetadata[_nftId] = metadata;
    
    emit NFTReceived(_recipient, _nftId, _sourceChainId);
}
```
</div>

### <svg width="25" height="25" viewBox="0 0 25 25" xmlns="http://www.w3.org/2000/svg" style="vertical-align: middle;">
  <text x="0" y="18" font-family="Arial, sans-serif" font-size="18" font-weight="bold" fill="#00E5E5">//</text>
</svg> Private Oracles

<div style="border-left: 3px solid #00E5E5; padding-left: 15px;">

Connect contracts to off-chain private data sources and APIs with secure oracles. Bring real-world data on-chain without compromising security.

```solidity
// Request data from private oracle
function requestWeather(string memory _zipcode) external returns (uint) {
    uint requestId = nextRequestId++;
    bytes memory featureData = abi.encode(requestId, _zipcode);
    _sendMessageWithFeature(
        block.chainid,
        "",
        1,  // Feature ID for Private Oracle
        featureData
    );
    emit WeatherRequested(requestId, msg.sender, _zipcode);
    return requestId;
}

// Process incoming data from oracle
function _processMessageWithFeature(
    uint, uint, bytes memory, uint32, bytes memory, bytes memory _featureResponse
) internal override {
    // Decode the feature response
    (uint requestId, string memory temperature, string memory conditions, string memory location) = 
        abi.decode(_featureResponse, (uint, string, string, string));
    
    // Store the weather data
    weatherRequests[requestId].temperature = temperature;
    weatherRequests[requestId].conditions = conditions;
    weatherRequests[requestId].location = location;
    weatherRequests[requestId].timestamp = block.timestamp;
    weatherRequests[requestId].fulfilled = true;
    
    emit WeatherReceived(requestId, temperature, conditions, location);
}
```
</div>

<br>

## Technical Architecture

VIA Protocol's architecture is built on three core components:

### 1. MessageClient

The `MessageClient` is a Solidity contract that provides a simple interface for cross-chain communication. It abstracts away the complexity of cross-chain messaging, allowing developers to focus on their application logic.

```solidity
// Send a message to another chain
_sendMessage(destChainId, abi.encode(data));

// Process incoming messages
function _processMessage(uint _sourceChainId, uint, bytes calldata _data) internal virtual override {
    // Decode and process the message
    (address recipient, uint amount) = abi.decode(_data, (address, uint));
    // Your logic here
}
```

### 2. Decentralized Validator Network

Our protocol is secured by a decentralized network of validators that ensure transaction integrity and provide multi-layer consensus. This network:

- Validates cross-chain messages
- Ensures message delivery
- Prevents double-spending
- Maintains network security

### 3. Private Oracles

Private Oracles allows for extensible functionality beyond basic messaging:

- **Private Datasources**: Connect smart contracts to off-chain databases or APIs
- **Custom Logic**: Implement complex cross-chain business logic
- **Real World Reach**: Communicate with real world devices through IoT APIs or embedded systems integrations

<br>

## Getting Started

Jump right in with our quickstart repositories:

<table>
<tr>
<td width="33%" style="border-left: 3px solid #00E5E5;">
<h3><a href="https://github.com/VIALabs-io/quickstart-token">Cross-Chain Token</a></h3>
<p>Create and deploy a cross-chain native ERC20 token in minutes.</p>

```bash
git clone https://github.com/VIALabs-io/quickstart-token.git
cd quickstart-token
npm install
node scripts/deploy.js
```
</td>
<td width="33%" style="border-left: 3px solid #FF00FF;">
<h3><a href="https://github.com/VIALabs-io/quickstart-nft">Cross-Chain NFT</a></h3>
<p>Build a cross-chain native NFT collection with metadata preservation.</p>

```bash
git clone https://github.com/VIALabs-io/quickstart-nft.git
cd quickstart-nft
npm install
node scripts/deploy.js
```
</td>
<td width="33%" style="border-left: 3px solid #00E5E5;">
<h3><a href="https://github.com/VIALabs-io/quickstart-oracle">Private Oracle</a></h3>
<p>Connect your contracts to off-chain data sources.</p>

```bash
git clone https://github.com/VIALabs-io/quickstart-oracle.git
cd quickstart-oracle
npm install
node scripts/deploy.js
```
</td>
</tr>
</table>

<br>



## 🔗 Resources

- [Developer Documentation](https://developer.vialabs.io)
- [GitHub Repositories](https://github.com/VIALabs-io)
- [Discord Community](https://discord.gg/vialabs)
- [Twitter](https://x.com/VIA_Labs)

<br>

<div align="center">
  <h2>Start Building Cross-Chain Today</h2>
  <p>Contact us at <a href="mailto:hello@vialabs.io">hello@vialabs.io</a> for collaborations and partnerships</p>
</div>
