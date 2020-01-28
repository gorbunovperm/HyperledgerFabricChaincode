# HyperledgerFabricChaincode
Test task from Optimum Software

## Terminal commands

### Terminal 1

docker-compose -f docker-compose-simple.yaml up

### Terminal 2

docker exec -it chaincode sh

go build -o optimum

CORE_PEER_ADDRESS=peer:7052 CORE_CHAINCODE_ID_NAME=optimum:0 ./optimum

### Terminal 3

docker exec -it cli bash

set -e
peer channel create -c myc -f myc.tx -o orderer:7050
peer channel join -b myc.block

peer chaincode install -p chaincodedev/chaincode/optimum -n optimum -v 0

peer chaincode instantiate -n optimum -v 0 -c '{"Args":["init","oauth_credentials"]}' -C myc

peer chaincode query -n optimum -c '{"Args":["getAuthUrl"]}' -C myc

peer chaincode invoke -n optimum -c '{"Args":["setVar","authToken","token_value"]}' -C myc

peer chaincode query -n optimum -c '{"Args":["getLabels"]}' -C myc
