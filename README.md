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

## Connecting Hyperledger Explorer to our network 
(Used for better front end visualization of channel, chaincodes, block data, transaction read/write states etc.)
1. Copy the name of the file under fabric-samples/test-network/organizations/peerOrganizations/org2.example.com/users/Admin@org2.example.com/msp/keystore/
(It should be something similar to this 8e98d26e813bbd63a9ad0df5f499101ce90e4bd28004435b229e5df1bf0fdeaf_sk)
2. Open the file test-network.json inside explorer/connection-profile
3. modify the value of key ("path") at line# 32. Replace the last part of the path with the name you just copied
4. Open a terminal inside the directory explorer and run the following to start the explorer
```
docker-compose up -d
```
5. Go to localhost:8080 and use 'exploreradmin' and 'exploreradminpw' (without the single quotations) as the username and password respectively 
6. To close the explorer, run the following inside the same directory
```
docker-compose down -v
```
