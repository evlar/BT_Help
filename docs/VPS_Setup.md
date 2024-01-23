
# Server Setup Instructions

## Provisioning a Server

Choose a server type (VPS or Bare Metal) that best fits your needs in terms of resources like CPU, RAM, and storage.

## Log in to the Server

```
ssh root@YOUR-IPADDRESS
```

## Update Linux

```
sudo apt update && sudo apt upgrade -y
```

## Install npm/pm2

PM2 is a production process manager for Node.js applications. It allows you to keep applications alive forever and reload them without downtime.

```
sudo apt install npm -y && sudo npm install pm2@latest -g && pm2 update
```

## Install TMUX and HTOP

TMUX is a terminal multiplexer, allowing you to run multiple terminal sessions inside a single window. HTOP is an interactive system-monitor process-viewer.

```
sudo apt install tmux && sudo apt install htop
```

## Install Pip

Pip is the package installer for Python. You can use it to install packages from the Python Package Index and other indexes.

```
sudo apt install python3-pip -y
```

## Install Bittensor

Bittensor is a decentralized neural network. With this, you can install and run Bittensor nodes.

```
python3 -m pip install bittensor
```