FlavorXL [FXL] 2021
===========================================================================================

http://flavorxl.com/

What is the FlavorXL [FXL] Blockchain?
-----------------------------------------

### Overview
FlavorXL is a blockchain project with the goal of creating a blockchain for the student, one where your degrees are stored on the blockchain and can be validated by employers by the pubkey that sent you the degree.

### Blockchain Technology
The FlavorXL [FXL] Blockchain is an experimental smart contract platform that enables 
instant payments to anyone, anywhere in the world in a private, secure manner. 
FlavorXL [FXL] uses peer-to-peer blockchain technology developed by CryptoCoderz and SaltineChips to operate
with no central authority: managing transactions, execution of contracts, and 
issuing money are carried out collectively by the network.

### Custom Difficulty Retarget Algorithm “VRX”
VRX is designed from the ground up to integrate properly with the Velocity parameter enforcement system to ensure users no longer receive orphan blocks.

### Velocity Block Constraint System
Ensuring FlavorXL stays as secure and robust as possible, we have implemented what's known as the Velocity block constraint system (developed by CryptoCoderz & SaltineChips). This system acts as a third and final check for both mined and peer-accepted blocks, ensuring that all parameters are strictly enforced.

### Wish (bmw512) Proof-of-Work Algorithm
Wish or bmw512 hashing algorithm is utilized for the Proof-of-Work function and also replaces much of the underlying codebase hashing functions as well that normally are SHA256. By doing so this codebase is able to be both exponentially lighter and more secure in comparison to reference implementations.

Specifications and General info
------------------
FlavorXL uses 

	libsecp256k1,
	libgmp,
	Boost1.74, OR Boost1.6,  
	Openssl1.02u,
	Berkeley DB 6.2.32,
	QT5.15.2,
	to compile


General Specs

	Coin Name: FlavorXL
	Ticker: FXL
	Block Spacing: 5 Minutes
	Stake Minimum Age: 80 Confirmations (PoS-v3) | 6 Hours (PoS-v2)
	PoW/PoS Reward: 1 FXL (Per-block)
	MasterNode Reward: 3.5 FXL (Per-block)
	DevOps Fees: 0.25 FXL (Per-block)
	Maximum Coin Count: 200 Million FXL
	Premine Coin Count: 100 Million FXL (used for - Airdrop (mostly), Graphics, Coding, and operating costs)
	Mineable/Mintable Coin Count: 100 Million FXL
	Port: 20299
	RPC Port: 20099


BUILD LINUX
-----------
### Compiling FlavorXL "SatoshiCore" daemon on Ubunutu 18.04 LTS Bionic
### Note: guide should be compatible with other Ubuntu versions from 14.04+

### Become poweruser
```
sudo -i
```
### CREATE SWAP FILE FOR DAEMON BUILD (if system has less than 2GB of RAM)
```
cd ~; sudo fallocate -l 3G /swapfile; ls -lh /swapfile; sudo chmod 600 /swapfile; ls -lh /swapfile; sudo mkswap /swapfile; sudo swapon /swapfile; sudo swapon --show; sudo cp /etc/fstab /etc/fstab.bak; echo '/swapfile none swap sw 0 0' | sudo tee -a /etc/fstab
```

### Dependencies install
```
cd ~; sudo apt-get install -y ntp git build-essential libssl-dev libdb-dev libdb++-dev libboost-all-dev libqrencode-dev libcurl4-openssl-dev curl libzip-dev; apt-get update -y; apt-get install -y git make automake build-essential libboost-all-dev; apt-get install -y yasm binutils libcurl4-openssl-dev openssl libssl-dev; sudo apt-get install -y libgmp-dev; sudo apt-get install -y libtool;
```

### Dependencies build and link
```
cd ~; wget http://download.oracle.com/berkeley-db/db-6.2.32.NC.tar.gz; tar zxf db-6.2.32.NC.tar.gz; cd db-6.2.32.NC/build_unix; ../dist/configure --enable-cxx --disable-shared; make; sudo make install; sudo ln -s /usr/local/BerkeleyDB.6.2/lib/libdb-6.2.so /usr/lib/libdb-6.2.so; sudo ln -s /usr/local/BerkeleyDB.6.2/lib/libdb_cxx-6.2.so /usr/lib/libdb_cxx-6.2.so; export BDB_INCLUDE_PATH="/usr/local/BerkeleyDB.6.2/include"; export BDB_LIB_PATH="/usr/local/BerkeleyDB.6.2/lib"
```

### GitHub pull (Source Download)
```
cd ~; git clone https://github.com/FlavorXL/FlavorXL-Core FlavorXL
```

### Build FlavorXL daemon
```
cd ~; cd ~/FlavorXL/src; chmod a+x obj; chmod a+x leveldb/build_detect_platform; chmod a+x secp256k1; chmod a+x leveldb; chmod a+x ~/FlavorXL/src; chmod a+x ~/FlavorXL; make -f makefile.unix USE_UPNP=-; cd ~; cp -r ~/FlavorXL/src/FlavorXLd /usr/local/bin/FlavorXLd;
```

### (Optional) Build FlavorXL-QT (GUI wallet) on Linux 

**All previous steps must be completed first.**

If you recompiling some other time you don't have to repeat previous steps, but need to define those variables. Skip this command if this is your first build and previous steps were performed in current terminal session.
```
export BDB_INCLUDE_PATH="/usr/local/BerkeleyDB.6.2/include"; export BDB_LIB_PATH="/usr/local/BerkeleyDB.6.2/lib"
```

With UPNP:

```
cd ~; cd ~/FlavorXL; qmake -qt=qt5; make
```

**Recommended Without** UPNP:

```
cd ~; cd ~/FlavorXL; qmake -qt=qt5 USE_UPNP=-; make
```



### Create config file for daemon
```
cd ~; sudo ufw allow 20299/tcp; sudo ufw allow 20099/tcp; sudo ufw allow 22/tcp; sudo mkdir ~/.FXL; cat << "CONFIG" >> ~/.FXL/FlavorXL.conf
listen=1
server=1
daemon=1
deminodes=1
demimaxdepth=200
testnet=0
rpcuser=FXLrpcuser
rpcpassword=SomeCrazyVeryVerySecurePasswordHere
rpcport=20099
port=20299
rpcconnect=127.0.0.1
rpcallowip=127.0.0.1
addnode=173.230.156.35:20299
addnode=172.105.121.51:20299
addnode=172.104.168.50:20299
CONFIG
chmod 700 ~/.FXL/FlavorXL.conf; chmod 700 ~/.FXL; ls -la ~/.FXL
```

### Run FlavorXL daemon
```
cd ~; FlavorXLd; FlavorXLd getinfo
```

### Troubleshooting
### for basic troubleshooting run the following commands when compiling:
### this is for minupnpc errors compiling

```
make clean -f makefile.unix USE_UPNP=-
make -f makefile.unix USE_UPNP=-
```
### Updating daemon in bin directory
```
cd ~; cp -r ~/FlavorXL/src/FlavorXLd /usr/local/bin
```

License
-------

FlavorXL [FXL] is released under the terms of the MIT license. See [COPYING](COPYING) for more
information or see https://opensource.org/licenses/MIT.

Development Process
-------------------

The `master` branch is regularly built and tested, but is not guaranteed to be
completely stable. [Tags](https://github.com/SaltineChips/FlavorXL/Tags) are created
regularly to indicate new official, stable release versions of FlavorXL [FXL].

The contribution workflow is described in [CONTRIBUTING.md](CONTRIBUTING.md).

The developer [mailing list](https://lists.linuxfoundation.org/mailman/listinfo/bitcoin-dev)
should be used to discuss complicated or controversial changes before working
on a patch set.

Developer Discord can be found at https://discord.gg/Jp2ujYH.

Testing
-------

Testing and code review is the bottleneck for development; we get more pull
requests than we can review and test on short notice. Please be patient and help out by testing
other people's pull requests, and remember this is a security-critical project where any mistake might cost people
lots of money.

### Automated Testing

Developers are strongly encouraged to write [unit tests](/doc/unit-tests.md) for new code, and to
submit new unit tests for old code. Unit tests can be compiled and run
(assuming they weren't disabled in configure) with: `make check`

There are also [regression and integration tests](/qa) of the RPC interface, written
in Python, that are run automatically on the build server.

### Manual Quality Assurance (QA) Testing

Changes should be tested by somebody other than the developer who wrote the
code. This is especially important for large or high-risk changes. It is useful
to add a test plan to the pull request description if testing the changes is
not straightforward.
