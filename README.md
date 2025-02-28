# sallmon_coin

#!/bin/bash

echo "🚀 Starting the SallmonCoin Installation Process..."

# ----------------------------
# 📌 Step 1: Update System
# ----------------------------
echo "🔄 Updating and upgrading system packages..."
sudo apt update
sudo apt upgrade -y

# ----------------------------
# 📌 Step 2: Install Required Dependencies
# ----------------------------
echo "📦 Installing build-essential..."
sudo apt install -y build-essential

echo "📦 Installing automake..."
sudo apt install -y automake

echo "📦 Installing autotools-dev..."
sudo apt install -y autotools-dev

echo "📦 Installing libtool..."
sudo apt install -y libtool

echo "📦 Installing pkg-config..."
sudo apt install -y pkg-config

echo "📦 Installing libssl-dev..."
sudo apt install -y libssl-dev

echo "📦 Installing libevent-dev..."
sudo apt install -y libevent-dev

echo "📦 Installing bsdmainutils..."
sudo apt install -y bsdmainutils

echo "📦 Installing software-properties-common..."
sudo apt install -y software-properties-common

echo "📦 Installing libboost-all-dev..."
sudo apt install -y libboost-all-dev

echo "📦 Installing libminiupnpc-dev..."
sudo apt install -y libminiupnpc-dev

echo "📦 Installing libzmq3-dev..."
sudo apt install -y libzmq3-dev

echo "📦 Installing qttools5-dev-tools..."
sudo apt install -y qttools5-dev-tools

echo "📦 Installing protobuf-compiler..."
sudo apt install -y protobuf-compiler

echo "📦 Installing libprotobuf-dev..."
sudo apt install -y libprotobuf-dev

echo "📦 Installing libqt5core5a..."
sudo apt install -y libqt5core5a

echo "📦 Installing libqt5dbus5..."
sudo apt install -y libqt5dbus5

echo "📦 Installing libqt5gui5..."
sudo apt install -y libqt5gui5

echo "📦 Installing libqt4-dev..."
sudo apt install -y libqt4-dev

echo "📦 Installing git..."
sudo apt install -y git

# ----------------------------
# 📌 Step 3: Fix BerkeleyDB 4.8 Issues
# ----------------------------
echo "🔹 Adding Bitcoin PPA for BerkeleyDB 4.8..."
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 8842CE5E
sudo add-apt-repository -y ppa:bitcoin/bitcoin
sudo apt update

echo "📦 Installing BerkeleyDB 4.8..."
sudo apt install -y libdb4.8-dev
sudo apt install -y libdb4.8++-dev

# ----------------------------
# 📌 Step 4: Clone SallmonCoin Repository
# ----------------------------
echo "🔹 Cloning SallmonCoin repository..."
cd ~/Desktop
git clone -b 0.8 https://github.com/litecoin-project/litecoin.git sallmoncoin
cd sallmoncoin

echo "🔹 Renaming Litecoin to SallmonCoin..."
find . -type f -print0 | xargs -0 sed -i 's/litecoin/sallmoncoin/g'
find . -type f -print0 | xargs -0 sed -i 's/Litecoin/SallmonCoin/g'
find . -type f -print0 | xargs -0 sed -i 's/LiteCoin/SallmonCoin/g'
find . -type f -print0 | xargs -0 sed -i 's/LITECOIN/SALLMONCOIN/g'
find . -type f -print0 | xargs -0 sed -i 's/LTC/SALL/g'

# ----------------------------
# 📌 Step 5: Compile SallmonCoin
# ----------------------------
echo "🔹 Compiling SallmonCoin..."
cd src
make clean
make -f makefile.unix -j$(nproc)

# ----------------------------
# 📌 Step 6: Run SallmonCoin
# ----------------------------
echo "🚀 Running SallmonCoin daemon..."
./sallmoncoind -daemon

echo "🎉 SallmonCoin is now installed and running!"
