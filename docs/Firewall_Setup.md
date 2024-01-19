# Configuring the Firewall:

## Here's how you can set up the rules using ufw:
- Default port for SSH connections (Port 22)

    ```bash
    sudo ufw allow 22/tcp             # SSH
    ```
- If running a local subtensor, open these ports:

    ```bash
    sudo ufw allow 9933/tcp          # Subtensor/Docker
    sudo ufw allow 9944/tcp          # Subtensor/Docker WebSocket
    sudo ufw allow 30333/tcp         # Subtensor/Docker P2P
    ```
- Open each miner's axon.port (E.g. 9000, 9001, 9002, ect.):
    ```bash
    sudo ufw allow 9000/tcp          # Axon Port
    sudo ufw allow 9001/tcp          # Axon Port
    sudo ufw allow 9002/tcp          # Axon Port
    ```
- Enable firewall and varify the status:
    ```bash
    sudo ufw enable                  # Enable the firewall
    sudo ufw status                  # Check the status and rules
    ```

Note: Before enabling the firewall, ensure that you have another way to access the server in case of SSH issues. After enabling the firewall, test each service to make sure it's accessible and functioning correctly.
