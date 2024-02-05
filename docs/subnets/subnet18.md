
# Setting Up VPS Miner on Bittensor Subnet 18

## Prerequisites

You'll need to install a few dependencies and set up your environment before you can start mining on the Bittensor Subnet 18. Follow the steps below to get started:

### Install Wandb

You'll need to install Wandb using pip. Wandb is a tool for machine learning experiment tracking.

```bash
pip install wandb
```

> [Wandb](https://pypi.org/project/wandb/) is a Python package for experiment tracking. You can find more information about it on its PyPI page.

### Log in to Wandb

After installing Wandb, you need to log in to your Wandb account from the terminal using the following command:

```bash
wandb login
```

> Make sure you have an account on [Wandb](https://wandb.ai/) and generate an API key before running this command.

### Clone and Install Cortex.t

Clone the Cortex.t repository from GitHub and install it:

```bash
git clone https://github.com/BitAPAI/cortex.t.git
cd cortex.t
pip install -e .
```

> This step clones the Cortex.t repository and installs the necessary Python packages.

### Configure Environment Variables

Add the following environment variables to your `~/.bashrc` file and source it to set the variables:

```bash
echo "export OPENAI_API_KEY=MYAPIKEYHERE" >> ~/.bashrc
echo "export STABILITY_KEY=MYAPIKEYHERE" >> ~/.bashrc
echo "export ANTHROPIC_API_KEY=MYAPIKEYHERE" >> ~/.bashrc
source ~/.bashrc
```

> Replace `MYAPIKEYHERE` with your actual API keys for OpenAI, Stability, and Anthropic.

### Install AWS CLI

Install the AWS Command Line Interface (CLI) and configure it:

```bash
pip install awscli
aws configure
```

> You may need to set up your AWS credentials and region during the configuration.

## Mining Setup

Now that you have the necessary dependencies installed and your environment configured, you can set up the miner for Bittensor Subnet 18:

### Set PYTHONPATH

From the cortex.t repository, export the `PYTHONPATH`:

```bash
cd cortex.t
export PYTHONPATH=/root/cortex.t
```

### Register Wallet and Delegate

Register your wallet and delegate to Subnet 18:

```bash
btcli s register --netuid 18 --wallet.name MYWALLET--wallet.hotkey MYHK
```

### Start Mining

You can start mining with the following commands, replacing placeholders with your wallet information and port number:

```bash
# Replace MYWALLET, MYHOTKEY, and MYPORTNUMBER with your wallet details and port number
pm2 start /root/cortex.t/miner/miner.py --interpreter python3 -- --netuid 18 --subtensor.network local --wallet.name MYWALLET --wallet.hotkey MYHOTKEY --axon.port MYPORTNUMBER
```

## Additional Considerations

### IP Identification Tools

Consider using IP identification tools to detect and mitigate bot attacks:

```bash
# Check active network connections
netstat -a

# Explore network tools for further analysis
nettools
```

### Miner Restart Reminder

After pulling updates from the repository, don't forget to restart your miner:

```bash
pm2 restart all --update-env
```

Now, you have successfully set up your VPS as a miner on Bittensor Subnet 18.


Make sure to replace `MYAPIKEYHERE`, `MYWALLET`, `MYHOTKEY`, and `MYPORTNUMBER` with your actual API keys, wallet information, and port number.
