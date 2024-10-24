# BlockChat
BlockChat is a decentralized messaging and transaction platform built using blockchain technology. It was created as part of the Distributed Systems course of the [School of Electrical and Computer Engineering](https://www.ece.ntua.gr/en) of the [National Technical University of Athens](https://ntua.gr/en/) during the academic year 2023-2024.

#### Contributors
`gkapetanakis` - George Kapetanakis (me)

#### Grade
The project was graded with a 10 out of 10.

## Jump to a Section
* [Repository Contents](#repository-contents)
* [What is BlockChat and how does it work?](#what-is-blockchat-and-how-does-it-work)
* [Additional Info](#additional-info)
* [Setup Guide](#setup-guide)
* [Usage Guide](#usage-guide)
* [Testing Guide](#testing-guide)

## Repository Contents
* `handouts`: The project description in both English and Greek.
* `src`: The project's source code, written in Rust.
* `test_inputs`: Files provided along with the project description, used to test the application.
* `compose.yaml`: This, along with the files in `dockerfiles`, are necessary for running the application locally using Docker.

## What is BlockChat and how does it work?
BlockChat is a decentralized messaging and transaction platform built on blockchain technology. It enables users to exchange messages and conduct transactions without the need for a central authority. BlockChat utilizes a simple blockchain to record transactions and messages exchanged among participants. It employs a Proof-of-Stake algorithm for consensus. The currency used in the transactions is called BlockChat Coin (BCC). Users can send text messages for a fee, send BCC for a fee, or stake BCC in order to be able to validate transactions and earn validation rewards.

The system is relatively simple and works as follows:
* Firstly, the number of users (which will be called __nodes__ for the rest of this section) participating in the system is known beforehand.
* Secondly, every node of the system knows the socket address of the first node of the network. This node is called the __bootstrap node__, as its responsibility is to bootstrap the network and initialize the blockchain.
* The bootstrapping process is as follows:
    * The bootstrap node starts listening on a socket address for join requests.
    * Each node of the system sends a join request containing their __socket address__ and their __wallet address__ (which is an RSA public key).
    * Once all the expected nodes have joined, the bootstrap node initializes the blockchain, giving every node a set amount of BCC (e.g. 1000 BCC). The blockchain, along with every node's socket/wallet address pair is then broadcast to everyone else.
* After the bootstrapping is complete, users are free to exchange text messages and send or stake coins.

What exactly is a node and how does a user interact with the system?
* A node is an executable intended to be run as a background service (__daemon__) on the user's machine. The user can then interact with this service using a CLI provided as a different executable.

If you want a more detailed explanation I suggest reading the source code. Check out `bin/daemon.rs`, `protocol.rs` and `bootstrap.rs` first. I've included detailed comments on every part of the code I deemed confusing or not having a clear rationale.

## Additional Info
* The project was originally set up and tested on the IaaS [~okeanos-knossos](https://okeanos-knossos.grnet.gr/about/what/) platform, access to which was provided by my university.
* The application is in no way meant to be used for actual messaging, as it __does not persist any data to disk__ and __is not secure__, among other reasons.

## Setup Guide
* Make sure you have Rust installed, or install it from [here](https://www.rust-lang.org/tools/install). The most recent version I've tested this project with is 1.78.0. Newer versions of the language will probably work as well.
* Download or clone this repository in a local folder. I will refer to this folder as `./`.
* Run `./cargo build` if to compile the source code. Three different binaries can be built, `daemon`, `client` and `helper`, which can be specified as follows if needed: `./cargo build --bin <binary_name>`. If you want to run any of the binaries you can use `./cargo run --bin <binary_name>`. There is not much point in building or running the application like this, as it requires multiple instances of itself, able to communicate with each other, to work.
* __[Recommended]__ To run the application locally without manually setting up multiple instances, you can use Docker. Just run `./docker compose up` and wait.

## Usage Guide
Will be updated soon.

## Testing Guide
Will be updated soon.
