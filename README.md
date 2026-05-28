# Go Ethereum (Geth) Node Setup Instructions

This guide provides the clean setup steps and node initialization commands for deploying the custom network node.

---

## 📦 1. Installation & Dependencies

Run the following commands to install Go Ethereum and manage repository updates:

```bash
sudo apt-get install software-properties-common
sudo add-apt-repository -y ppa:ethereum/ethereum
sudo apt-get update
sudo apt-get install ethereum
sudo apt-get upgrade geth

# Allow Port From Server Incoming & Outgoing

sudo ufw allow http
sudo ufw allow https
sudo ufw allow 8085/tcp
sudo ufw allow 9095/tcp
sudo ufw allow 30305/tcp

# Extract the tarball
sudo tar -xvf geth-linux-amd64-1.10.15-8be800ff.tar.gz 

# Step into the extracted folder
cd geth-linux-amd64-1.10.15-8be800ff 

# Make the geth file executable
sudo chmod +x geth

# Copy the binary file to the user bin space
sudo cp geth /usr/local/bin/

# Initialize the node configuration
geth init --datadir node1 biten.json

# Step into the workspace
cd node1

# Start the node with consensus parameters, RPC, WebSockets, and mining flags
geth --nodiscover --syncmode full --allow-insecure-unlock --ws --ws.addr 0.0.0.0 --ws.port 9095 --ws.rpcprefix "/" --ws.origins "*" --http.rpcprefix "/" --http --http.api eth,web3,miner,admin,personal,net,db --http.rpcprefix "/" --http.vhosts "*" --http.addr "0.0.0.0" --http.corsdomain "*" --http.port 8085 --nat "any" --http.api eth,web3,miner,admin,txpool,debug,personal,net --ipcpath /data/btnnode/geth.ipc --datadir "./" --port 30305 --networkid 2026 --mine --miner.threads=1 --miner.etherbase=0xaddress


geth attach https://rpc.biten.io
# Or
geth attach http://185.192.97.41:8085


admin.addPeer("enode://15218c0feaffd86e0014cde5dd4c1cfe4a4d885b30783008f717c56bb71ffbde876e214b8b46475b94e89a499def600a8847d729c26a201089c974257cd5f8c6@185.192.97.41:30305?discport=0")
