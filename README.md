# Qiibee-QBX-contract
Audit smart contract 


## what is QBX?
QBX files facilitate sharing of financial data with accountants or users who don't have access to your main company file.

## How many part this contract have?
- contract Context
- interface IERC20 
- interface IERC20Metadata 
- contract ERC20
- contract Ownable
- interface IDexRouter
- interface IDexFactory
- contract QBX

#### contract Context
- **use case:**
The Context contract is commonly inherited by other contracts, particularly those that implement access control or require information about the transaction context.
It enhances the readability and maintainability of the code by encapsulating the logic for retrieving the sender and data. 

- **summary:**
The Context contract serves as a foundational component for building more complex contracts in Solidity, ensuring that developers have a reliable way to access transaction-related information while promoting cleaner code practices.


#### interface IERC20 

- **overview:**
The IERC20 interface defines the standard functions and events required for an ERC20 token in the Ethereum blockchain. ERC20 is a widely adopted standard that enables interoperability between various tokens and decentralized applications (dApps).

- **summary:**
The IERC20 interface is a fundamental component of the ERC20 token standard, providing a clear and consistent API for token contracts. By implementing this interface, developers ensure that their tokens are compatible with various wallets, exchanges, and dApps, promoting seamless interaction within the Ethereum ecosystem.


#### interface IERC20Metadata 

- **overview:**
The IERC20Metadata interface extends the basic IERC20 interface by adding functions that provide additional information about the token. This interface is part of the ERC20 token standard, which is widely used for creating fungible tokens on the Ethereum blockchain.


- **summary:**
The IERC20Metadata interface is an important extension of the ERC20 standard, providing essential metadata functions that enhance the usability and interoperability of tokens within the Ethereum ecosystem. By implementing this interface, developers ensure that their tokens are not only functional but also user-friendly and easily recognizable.


#### contract ERC20

- **overview:**
The ERC20 contract is an implementation of the ERC20 token standard, which defines a set of rules for creating fungible tokens on the Ethereum blockchain. This contract provides a complete and functional token that adheres to the ERC20 interface and includes essential features such as token transfers, allowances, and metadata.

- **summary:**
The ERC20 contract is a versatile and widely adopted implementation of the ERC20 token standard, enabling developers to create fungible tokens that can be utilized across a wide range of applications in the blockchain space. Its standardization promotes interoperability and ease of use, making it a cornerstone of the Ethereum ecosystem.


#### contract Ownable

- **overview:**
The Ownable contract is a utility contract that provides basic access control functionality, ensuring that only a designated owner can execute specific functions. It is commonly used in smart contracts to manage permissions and ownership.

- **summary:**
The Ownable contract is a foundational component for implementing ownership and access control in smart contracts, providing a simple and effective way to manage permissions and enhance security in decentralized applications.


#### interface IDexRouter

- **overview:**
The IDexRouter interface defines the essential functions for interacting with a decentralized exchange (DEX) router. This interface is critical for enabling token swaps and liquidity provision in decentralized finance (DeFi) applications.

- **summary:**
The IDexRouter interface is a crucial component for enabling seamless interactions with decentralized exchanges. It provides the necessary functions for token swaps and liquidity management, playing a vital role in the functionality of DeFi applications and enhancing the overall user experience in the decentralized finance ecosystem.

#### interface IDexFactory

- **overview:**
The IDexFactory interface defines the essential function for creating trading pairs on a decentralized exchange (DEX). This interface is crucial for enabling the creation of liquidity pools and facilitating token trading in decentralized finance (DeFi) applications.

- **summary:**
The IDexFactory interface is a crucial component for enabling the creation of trading pairs on decentralized exchanges. It simplifies the process of adding new tokens to the DEX and ensures that there is always a market for those tokens, promoting liquidity and trading opportunities within the DeFi ecosystem.

## Main Contract
#### contract QBX

- **Overview:**
The QBX contract is a custom ERC20 token that implements additional features for managing trading, fees, and liquidity on a decentralized exchange (DEX). It extends the functionality of standard ERC20 tokens by incorporating ownership control, trading limits, and automated market-making capabilities.

- **Key Features:**
- Trading Control: The contract includes mechanisms to enable or disable trading, set maximum buy/sell amounts, and manage wallet limits to prevent excessive token accumulation.
- Fee Management: It allows the owner to set transaction fees for buying and selling tokens, which can be collected for treasury purposes.
- Liquidity Management: The contract interacts with a DEX router and factory to create liquidity pools, add liquidity, and facilitate token swaps.
- Treasury Management: It has a designated treasury address for collecting fees and managing funds, with functions to withdraw tokens and ETH.
- Automated Market Maker Integration: The contract supports automated market maker pairs, allowing for seamless trading on DEX platforms.

- **Use Cases:**
- Token Launch: The QBX contract can be deployed to create a new token, allowing users to buy, sell, and trade the token on decentralized exchanges.
- Decentralized Finance (DeFi): The contract can be utilized within DeFi ecosystems for liquidity provision, yield farming, and other financial activities, enabling users to earn rewards.
- Community Governance: By implementing ownership control, the contract allows for community-driven governance, where token holders can vote on changes to fees, limits, and other parameters.
- Treasury Management: The contract's treasury functionality enables efficient management of collected fees, allowing for reinvestment or distribution to stakeholders.
- Market Stability: The limits on trading and wallet sizes help maintain market stability and prevent price manipulation, contributing to a healthier trading environment.

- **Conclusion:**
The QBX contract is a versatile and feature-rich ERC20 token implementation that provides essential tools for managing trading, liquidity, and treasury functions within a decentralized finance context. Its design promotes security, flexibility, and community engagement, making it suitable for a wide range of applications in the blockchain ecosystem. Feel free to send specific functions one by one, and I'll provide detailed insights and explanations for each!


#### Contract Variables:
##### Trading Limits
- **maxBuyAmount:** The maximum amount of tokens that can be bought in a single transaction.
- **maxSellAmount:** The maximum amount of tokens that can be sold in a single transaction.
- **maxWalletAmount:** The maximum amount of tokens that can be held in a single wallet.

##### DEX Integration
- **uniswapV2Factory:** The address of the Uniswap V2 factory contract.
- **uniswapV2Router:** The address of the Uniswap V2 router contract.
- **uniswapV2Pair:** The address of the Uniswap V2 trading pair for the token.
- **WETH:** The address of the Wrapped Ether (WETH) token.

##### Trading Control
- **swapping:** A boolean flag indicating whether the contract is currently swapping tokens.
- **swapTokensAtAmount:** The threshold amount of tokens that triggers a swap when exceeded.
- **tradingActiveBlock:** The block number at which trading was activated.
- **limitsInEffect:** A boolean flag indicating whether trading limits are in effect.
- **tradingActive:** A boolean flag indicating whether trading is active.
- **swapEnabled:** A boolean flag indicating whether token swapping is enabled.

##### Fees Management
- **buyFee:** The fee percentage charged on token purchases.
- **sellFee:** The fee percentage charged on token sales.
- **tokensForTreasury:** The number of tokens collected as fees for the treasury.

##### Exclusions and Limits
- **_isExcludedFromFees:** A mapping that tracks addresses excluded from paying fees.
- **_isExcludedMaxTransactionAmount:** A mapping that tracks addresses excluded from transaction limits.
- **automatedMarketMakerPairs:** A mapping that tracks automated market maker pairs.


#### Contract Mappings:
```shell
mapping (address => bool) private _isExcludedFromFees;
```
**Purpose:** This mapping tracks addresses that are exempt from paying transaction fees. This is useful for specific accounts, such as the contract owner or liquidity pools, to facilitate transactions without incurring fees.
```shell

mapping (address => bool) public _isExcludedMaxTransactionAmount;
```
**Purpose:** This mapping tracks addresses that are exempt from maximum transaction limits. This allows certain addresses (like the owner or liquidity pools) to bypass restrictions that apply to regular users, ensuring they can operate without limitations.

```shell
mapping (address => bool) public automatedMarketMakerPairs;
```
**Purpose:** This mapping identifies addresses that represent automated market maker pairs (e.g., liquidity pools on a DEX). Transfers to these addresses may be subject to specific restrictions, such as maximum transfer amounts, to prevent large trades that could destabilize the market.

#### Security Considerations
- **Access Control:** Ensure that only authorized addresses (e.g., the contract owner) can modify the mappings to prevent unauthorized changes that could exploit the contract.
- **Input Validation:** When adding or removing addresses from these mappings, implement checks to prevent invalid addresses (e.g., zero address) from being included.
- **Event Emission:** Emit events when addresses are added or removed from these mappings to maintain transparency and allow for tracking changes.

#### Gas Optimization Considerations
- **Mapping Efficiency:** Mappings are inherently efficient for storage and retrieval, but ensure that they are not overly complex or used excessively to avoid unnecessary gas costs.
- **Batch Updates:** If multiple addresses need to be updated in the mappings, consider implementing batch functions to reduce the number of transactions and save gas.


#### constructor

The constructor of the QBX contract effectively sets up the token's identity, establishes trading parameters, integrates with a decentralized exchange, and configures ownership and fee structures. This foundational setup is crucial for the contract's functionality and ensures that the token operates smoothly within the Ethereum ecosystem.





## vulnerabilities
```shell
function updateMaxBuyAmount(uint256 newNum) external onlyOwner {}
```

- **problem:** Lack of Upper Limit on newNum:
- **Explanation:** There is no upper limit on the newNum value. The owner could set it to an excessively high value, which might lead to unintended consequences in trading.
- **example:** 
If the owner mistakenly sets a very low maximum buy amount, it could prevent legitimate trading and cause dissatisfaction among users.

- **solutions:** 
    - Implement Multi-Signature Control: Use a multi-signature wallet for ownership to reduce the risk of a single point of failure.
    - Add Upper Limit Checks: Ensure that the new maximum buy amount is not only above a minimum threshold but also below a reasonable maximum.
    - Provide Reversion Mechanisms: Consider allowing the owner to revert changes to critical parameters or implement a delay before changes take effect to allow for community feedback.
    - Regular Audits: Conduct regular audits of the contract to identify potential vulnerabilities and ensure that best practices are being followed.

- **Summary of Attack Scenario:**
An attacker compromises the owner's private key.
They set the maximum buy amount to a very low value (e.g., 1 token).
Legitimate users find that they cannot buy tokens due to the low limit, causing frustration and potentially leading to a loss of trust in the token.
Alternatively, if the attacker sets an excessively high buy limit, it could lead to market manipulation or exploitative trading practices.


________________________
```shell
function setFees(uint256 _buyFee, uint256 _sellFee) external onlyOwner {}
```

- **problems:** 
    - he owner can set the fees to any value between 0% and 30%. If the owner's private key is compromised, an attacker could set the fees to the maximum allowed (30%), effectively draining funds from users who attempt to trade.
    - While the function checks that fees do not exceed 30%, there is no restriction on how frequently or drastically the owner can change the fees. This could lead to rapid fluctuations in fees that confuse or frustrate users.
    - If the owner sets the fees to a high value, it can discourage trading and lead to market manipulation. For example, if the buy fee is set to 30%, users would be discouraged from buying the token, leading to decreased liquidity and potential price drops.

- **solutions:** 
    - Consider implementing a multi-signature wallet for ownership or adding a mechanism to limit how much the buy/sell fees can be changed at once.
    - Implement a cooldown period between fee changes or set a maximum percentage increase or decrease allowed at one time.
    - Consider adding community governance features where token holders can vote on fee changes, or implement a mechanism to automatically adjust fees based on trading volume or other metrics.

- **Summary of Attack Scenario:**
An attacker gains access to the owner's private key.
They set the buy and sell fees to the maximum allowed (30%).
Users attempting to trade find that they are charged excessive fees, leading to significant losses.
This could discourage trading, manipulate the token's price, and damage the token's reputation.

________________________
```shell
function removeLimits() external onlyOwner {}
```
- **problems:** 
    - Once limits are removed, there is no built-in mechanism to revert this action or to re-enable limits without redeploying the contract.
    - This could lead to a situation where the contract operates without any trading limits indefinitely, which could be detrimental to the token's market stability.

- **solutions:** 
    - Add a Reversion Mechanism
    - Community Governance:
    - mplement Multi-Signature Control
________________________
