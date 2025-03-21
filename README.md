# **LayerEdge CLI Verifier**

## 1. Install Dependencies
Install Go 1.18 or higher (so I installed the latest version 1.24.1 instead)
````
LATEST_GO_VERSION=$(curl -s https://go.dev/VERSION?m=text)
wget https://go.dev/dl/${LATEST_GO_VERSION}.linux-amd64.tar.gz
sudo tar -C /usr/local -xzf ${LATEST_GO_VERSION}.linux-amd64.tar.gz
export PATH=$PATH:/usr/local/go/bin
echo 'export PATH=$PATH:/usr/local/go/bin' >> ~/.bashrc
source ~/.bashrc
````
Install Rust (1.81.0 or higher)
````
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
source ~/.cargo/env
````
Install risc0 Toolchain
````
curl -L https://risczero.com/install | bash && rzup install
````

## 2. Clone LightNode Repo
````
git clone https://github.com/Layer-Edge/light-node
cd light-node/
````

## 3. Configure Environment Variables
I use vim editor
````
vi .env
````
Press "i" to insert text 
````
GRPC_URL=grpc.testnet.layeredge.io:9090
CONTRACT_ADDR=cosmos1ufs3tlq4umljk0qfe8k5ya0x6hpavn897u2cnf9k0en9jr7qarqqt56709
ZK_PROVER_URL=http://127.0.0.1:3001
API_REQUEST_TIMEOUT=100
POINTS_API=http://127.0.0.1:8080
PRIVATE_KEY='cli-node-private-key'
````
* Paste (Ctrl+V or Ctrl+Shift+V)

* Edit `cli-node-private-key` and paste the evm privatekey you wish to use for your CLI

- Press "Esc" then Shift+Z+Z to save and exit editor


## 4. Clean Up
Update `go.mod` file
````
go mod tidy
````

## 5. Run the ZK Prover Server
Navigate to the risc0-merkle-service directory and start the prover:
````
cd risc0-merkle-service
cargo build && cargo run
````

## 6. Run the Light Node
Open a new SSH session or terminal and navigate to the project root:
````
cd light-node/
go build
./light-node
````

## 7. Monitoring & Troubleshooting
Check logs for errors:
````
tail -f logs.txt
````
