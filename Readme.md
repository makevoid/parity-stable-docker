# parity-stable-docker

Docker automated build containing a quite light (not alpine but still...) debian based container with parity installed, compiled from source

Current version is 1.7.0 (stable) pulled from github.

Downside: long build time (if you have to build it yourself)

Upside: pull it from dockerhub, it should be quite small (<50MB)


#### Notes:

Use this command to build the container and run a parity test network:

    docker build -t=parity . && docker run -p 30303:30303 -p 8545:8545 parity parity --chain dev --network-id 15623918910 -l ALL

Create a key:

    docker run -v $PWD/keys:/root/.local/share/io.parity.ethereum/keys/DevelopmentChain -ti parity parity --chain dev account new

Run unlocking the account:

    docker run -p 30303:30303 -p 8545:8545 --network=rodeth -v $PWD/config:/config -v $PWD/keys:/root/.local/share/io.parity.ethereum/keys/DevelopmentChain parity parity --chain dev --network-id 15623918910 -l ALL --unlock 0xed7835ae7f996067349ba9c3ae4da0fd5aeb0da3 --password /config/password --jsonrpc-interface 0.0.0.0

    docker run -p 30303:30303 -p 8545:8545 --network=rodeth -v $PWD/config:/config -v $PWD/keys:/root/.local/share/io.parity.ethereum/keys/DevelopmentChain parity parity --chain dev --network-id 15623918910 -l ALL --unlock 0x00a329c0648769a73afac7f9381e08fb43dbea72 --password /config/password --jsonrpc-interface 0.0.0.0
