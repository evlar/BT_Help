
# Setting Up a Subtensor Node Using Docker

## Step 1: Install Git
1. **Update Package Lists** (optional but recommended):
   ```
   sudo apt update
   ```
2. **Install Git**:
   ```
   sudo apt install git
   ```

## Step 2: Install Docker Engine
1. **Install Docker**:
   Since you're using Ubuntu, you can install Docker using these commands:
   ```
   sudo apt-get update
   sudo apt-get install apt-transport-https ca-certificates curl software-properties-common
   curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
   sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
   sudo apt-get update
   sudo apt-get install docker-ce
   ```
   After installation, verify that Docker is running:
   ```
   sudo systemctl status docker
   ```
   (You should see an output indicating that Docker is active and running.)

## Step 3: Run node-subtensor Container
1. **Clone the Subtensor Repository**:
   ```
   git clone https://github.com/opentensor/subtensor.git
   cd subtensor
   ```
2. **Run the Node**:
   Now, you can start the Subtensor node. For a mainnet lite node, use:
   ```
   sudo ./scripts/run/subtensor.sh -e docker --network mainnet --node-type lite
   ```
  
   Choose the appropriate command based on whether you want a mainnet/testnet and lite/archive node.
   See additional commands at https://github.com/opentensor/subtensor/blob/main/docs/running-subtensor-locally.md#running-docker
