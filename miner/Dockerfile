FROM ubuntu:xenial

RUN apt-get update \
     && apt-get install -y wget software-properties-common \
     && rm -rf /var/lib/apt/lists/*

WORKDIR "/root"

RUN add-apt-repository -y ppa:ethereum/ethereum

ARG binary
RUN apt-get update \
     && apt-get install -y ethereum

ARG password
ARG privatekey
RUN echo $password > ~/.accountpassword
RUN echo $privatekey > ~/.privatekey
#ADD ./genesis.json ./genesis.json
ADD ./nymbus.json ./genesis.json
RUN geth init genesis.json
RUN geth account import --password ~/.accountpassword  ~/.privatekey

#ENV address=""
#ENV bootnodeId=""
#ENV bootnodeIp=""

CMD exec geth --bootnodes "enode://$bootnodeId@$bootnodeIp:30301" --networkid "6669990001" --verbosity=4 --rpcaddr "0.0.0.0" --syncmode=full --mine --gasprice "0" --etherbase $address --unlock $address --password ~/.accountpassword
