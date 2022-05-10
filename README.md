# vaccine-supply-chain-HLF
(Assuming you have already installed the pre-requisites and binaries -- v2.2.5 as the Fabric version & v1.5.2 as the Fabric CA version)
## Bringing up the network
1. Clone the above repo and go inside fabric-samples/commercial-paper directory
2. Open a terminal here and run the following commands:-
```
./network-clean.sh
./network-starter.sh
```
The above brings up a fabric network with 3 organisations and 1 channel.

## Installing the "Covishield" chaincode on all the 3 organisation peers
Go inside fabric-samples/test-network directory, open a terminal here and run the following:-
```
bash scripts/deployCC.sh mychannel Covishield ../commercial-paper/organization/magnetocorp/contract/ javascript 1 1
```
This installs the smart contract and now client applications from either of the organisations can invoke the functions defined in contracts

## Creating identities (to use client applications) and importing them into wallets for each organisation
Open a terminal in the root of the project and run the following:-
```
cd fabric-samples/commercial-paper/organization/Org3/application
node enrollUser.js

cd ../../digibank/application
node enrollUser.js

cd ../../magnetocorp/application
node enrollUser.js
```

## Now we can run various client applications as defined in application folder of respective orgs
For example

Open terminal inside fabric-samples/commercial-paper/organization/magnetocorp/application directory and run
```
node issueFrontend.js
```
Inside fabric-samples/commercial-paper/organization/digibank/application directory
```
node buyFrontend.js
```
