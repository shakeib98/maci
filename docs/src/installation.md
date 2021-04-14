# Installation

## Requirements

You need the following to use MACI:

- An x86-64 system
- A Linux system, preferably a Debian-based distribution like Ubuntu
- NodeJS. Use [`nvm`](https://github.com/nvm-sh/nvm) to install it. MACI has
  been tested with Node 15.
- The `libgmp-dev` `nlohmann-json3-dev` `nasm` and `g++` Debian/Ubuntu
  packages. They are needed to run `circom-helper`, which in turn is used to
  develop and test zk-SNARK circuits.
- The [`rapidsnark`](https://github.com/iden3/rapidsnark) tool.


## Installation

### Install `rapidsnark`

First, install dependencies:

```bash
sudo apt-get install build-essential libgmp-dev libsodium-dev nasm git
```

Next, clone `rapidsnark` and build it:

```bash
git clone https://github.com/iden3/rapidsnark.git && \
cd rapidsnark && \
git checkout 1c13721de4a316b0b254c310ccec9341f5e2208e

npm install && \
git submodule init && \
git submodule update && \
npx task createFieldSources && \
npx task buildProver
```

Note the location of the `rapidsnark` binary (e.g.
`/home/user/rapidsnark/build/prover`).

### Install MACI

```bash
git clone https://github.com/appliedzkp/maci.git && \
cd maci && \
npm i && \
npm run bootstrap && \
npm run build
```

Install dependencies for `circom-helper`:

```bash
sudo apt-get install libgmp-dev nlohmann-json3-dev nasm g++
```

### Download `.zkey` files

MACI has two zk-SNARK circuits. Each circuit is parameterised. There should one
`.zkey` file for each circuit and set of parameters.

Unless you wish to generate a fresh set of `.zkey` files, you should obtain
them from someone who has performed a multi-party trusted setup for said
circuits..

Note the locations of the `.zkey` files as the CLI requires them as
command-line flags.