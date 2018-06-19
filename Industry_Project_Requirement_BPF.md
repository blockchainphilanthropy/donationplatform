# Industry Project

## Client
---

Blockchain Philanthropy Foundation is a not for profit organization
founded by a group of volunteers who are passionate about technology and
humanitarian causes. Our mission is to enable and accelerate
humanitarian projects and initiatives worldwide, through blockchain
technology.

We work with various industry partners and government bodies to raise
the awareness of Blockchain technology, educate the general public on
the benefit of blockchain technology for social good. We also contribute
to the Blockchain ecosystem by supporting the development of new
infrastructure and applications that help society globally benefit from
blockchain and related technology.

## Vision
---

__A web-based cryptocurrency donation platform to enable charities to receive digital currency donations__

The Foundation aims to:

-   Increase the amount of charity giving in the world

-   Restore public trust and confidence with great transparency

-   Reduce charitable fraud and waste

-   Increase donor engagement by allowing them to view and participate
    in the success of the programs they participate in.

-   Enable charities that are not tech savvy to participate in
    Blockchain technology and accept digital, physical and intangible
    assets including cryptocurrency

-   Provide reporting dashboard for both charities and individual donors
    to track donations

# Requirements
---

## Platform Actors

- Site administrator
  - Administers website and storage of user data


- Charity administrator
  - Creates and manages a donation campaign
  - Provides cryptocurrency target addresses (depending on solution)
  - Run reports on campaigns


- Donators
  - Uses website to donate to a campaign
  - Run personal reports

## Minimum Acceptance Criteria

1. Platform displays a list of charities and their donation addresses
2. Donator can send a transaction to a selected cryptocurrency address for a given charity
3. Platform can read blockchain and record transactions for each charity
4. Charities may login to platform and report on total donations
5. Donators may login to platform and report on their individual donations

## Detailed Requirements

### 1. Platform displays a list of charities and their donation addresses

#### Core

Platform must display a unique cryptocurrency address for a list of charities. The platform must have a database to record a least one address per charity.

#### Stretch
- Allow charities to login and set their own cryptocurrency address(es)
- _Generate_ and record in the platform's database, a unique addresses per donator per charity. This allows for more fine-grained transaction and blockchain reporting
- Allow the platform to work with multiple cryptocurrencies
- Allow charities to create and run "campaigns". A campaign will allow multiple donation streams for the one charity, with different goals, cryptocurrency addresses, and a method to differentiate between these sources in all functionality and reporting

### 2. Donator can send a transaction to a selected cryptocurrency address for a given charity

#### Core

A valid address for the given charity displayed on the platform for the donator to send to. At minimum level, this would be asynchronous and the platform would later interrogate the blockchain to verify completion.

#### Stretch
- Every donation uniquely tied to the donator and recorded in database for reporting
- In-place transaction verification. Some e-commerce plugins allow for in-place waits and popups for every transaction.

### 3. Platform can read blockchain and record transactions for each charity

#### Core

This is the main requirement and technical complexities of the project. Platform must be able to recognize a transaction (donation) has is pending or is confirmed, and record this in a database. There are many ways to go about this.

In order of difficulty/complexity:

 - Integrate an off-the-shelf e-commerce suite plugin
 - Integrate a commercial payment processor (for example [Bitpay](https://bitpay.com/), [Coinbase Commerce](https://commerce.coinbase.com/), etc) with the platform
 - Have the platform consume third-party APIs which query the blockchain for you - [Etherscan APIs](https://etherscan.io/apis), [Infura](https://infura.io/), [Blockchain.info](https://blockchain.info/api), etc
 - Run a full node on external servers and write and expose your own APIs to query blockchain(s)

Regardless of the method of querying the blockchain(s), the platform must be able to record the transaction was completed or abandoned by the donator, when it occurred, and which charity it was for.

#### Stretch
- Allow the platform to work with multiple cryptocurrencies

### 4. Charities may login to platform and report on total donations

#### Core

- Charities must be able to login to the platform and report on their total donations to date
- Report may be in any reasonable format, CSV, PDF, etc
- Report must show both cryptocurrency and fiat dollar (AUD) values _for the date the crypto was received_. This is crucial for accurate tax reporting, especially for organizations with charity status. Depending on the blockchain solution used (plugin or manually managed), platform may need to query price APIs to get this information.
- Two excellent free price APIs are [Coinmarketcap](https://coinmarketcap.com/api/) and [Cryptocompare](https://min-api.cryptocompare.com/)

#### Stretch
- If the "campaign" model has been used, reporting must show break down between different donation streams for the charity
- Create reports in different fiat currencies (JPY, EUR, USD) for internationalization, future platform scope

### 5. Donators may login to platform and report on their individual donations

#### Core
- Donators must be able to login to the platform and report on their total donations to date
- Report may be in any reasonable format, CSV, PDF, etc
- Report must show both cryptocurrency and fiat dollar (AUD) values _for the date the crypto was received_. This is crucial for accurate tax reporting, especially for organizations with charity status. Depending on the blockchain solution used (plugin or manually managed), platform may need to query price APIs to get this information.
- Two excellent free price APIs are [Coinmarketcap](https://coinmarketcap.com/api/) and [Cryptocompare](https://min-api.cryptocompare.com/)

#### Stretch
- If the "campaign" model has been used, reporting must show break down between different donation streams for the charity
- Create reports in different fiat currencies (JPY, EUR, USD) for internationalization, future platform scope.

## Charities and assets

Charity names, causes, images, and any other assets may be mocked up, however ideally in a way that allows for content management. An off-the-shelf e-commerce suite with built in customer relationship management may already include sections for branding and content management.

## Campaign model

The charity campaign concept should be added once the core requirements are fulfilled.

Campaigns might involve:
- Different content/assets for a charity
- Financial goals (raise $1M for a new hospital) and closure dates
- Gamification / donator engagement
- Breakdown to campaign level in all reporting

## Blockchain
---

The Foundation is agnostic on which cryptocurrency is used in the platform. The stretch scope is always that multiple cryptocurrencies would be accepted, e.g. Bitcoin, Ethereum, Litecoin, Bitcoin Cash. These are some of the largest projects by market cap and have a good range of tools and merchant acceptance. There are many exciting new projects with different value propositions, so I would recommend searching them out.

Initially though, recommendation is to focus on a well-known cryptocurrency with good developer tools, Bitcoin and Ethereum are great in this regard. Some off-the-shelf solutions may already have multiple currencies included, and you may not have to make this decision.

This is more of an integration project between a few different existing web technologies, with a blockchain element that displays and monitors transactions in an essentially centralised way. Portions of this could be written in smart contracts, especially on the Ethereum and EOS chains, but liveness/responsiveness of a web solution reading/writing data immediately on-chain would make for a poor user experience and isn't required (and may be prohibitively expensive).

## Security & Authorization
---

While user management is not explicitly mentioned, it is implied there is a login/authorization user story for all actors on the platform. Recommendation is not to reinvent the wheel and check out the many great resources out there, including SaaS authorization/user-management platforms like [Okta](https://developer.okta.com/) or [Auth0](https://auth0.com/pricing) both with free tiers for developers.

For those using cloud infrastructure, consider integrating [AWS Cognito](https://aws.amazon.com/cognito/) or [Azure AD](https://azure.microsoft.com/en-au/services/active-directory/). If stuck for time, a mocked up login/password store in your database is fine to demonstrate the core platform works - in a production system we will of course drop in an enterprise-grade solution as above.

## Technology Stack
---
The Blockchain Philanthropy Foundation itself is a not-for-profit and would prefer open-source technologies with open and/or free licensing. Additionally, consider technologies with very large developer bases and support/documentation.

## Useful References
---
- Developer resources for Bitcoin - https://github.com/ChristopherA/Blockchain-Developer-Resources

- Curated list of general blockchain information. This list is extremely comprehensive, skip the exchange and market information and check out the _Learning_, _Useful Tools_, and _For Developers_ sections - https://github.com/coinpride/CryptoList

- Example e-commernce suite with Reaction Commerce - creating a custom payment provider - https://docs.reactioncommerce.com/reaction-docs/master/creating-a-payment-provider

- Great list of Ethereum/Crypto terms - https://kb.myetherwallet.com/getting-started/ethereum-glossary.html

- List of charity donation platforms for inspiration - http://www.changepath.com.au/blog/2017/05/australian-charity-donation-platforms/
