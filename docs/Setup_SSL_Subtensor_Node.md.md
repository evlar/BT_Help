
# "Nginx SSL Setup with Let's Encrypt and Snap"

## 1. Setting Up a Subdomain and DNS 'A' Record
- **Purchase a Domain Name**: Setup a domain name with a domain registrar, like GoDaddy, Namecheap, or Google Domains.
- **Create a Subdomain**: Log into your domain management service and create a new subdomain (e.g., `node1.yourdomain.com`).
- **DNS 'A' Record**: Create a DNS 'A' record for the subdomain, pointing it to the IP address of your server.

## 2. Install Nginx on Your Server
- **Update package lists**:
  ```
  sudo apt update
  ```
- **Install Nginx**:
  ```
  sudo apt install nginx
  ```

## 3. Start and Enable Nginx
- **Start Nginx service**:
  ```
  sudo systemctl start nginx
  ```
- **Enable Nginx to start on boot**:
  ```
  sudo systemctl enable nginx
  ```

## 4. Firewall Adjustments
- **Allow HTTP and HTTPS traffic**:
  ```
  sudo ufw allow 'Nginx Full'
  sudo ufw reload
  ```
- **Enable the firewall** (if not already enabled):
  ```
  sudo ufw enable
  ```
- **Allow SSH** (to ensure remote access is not blocked):
  ```
  sudo ufw allow ssh
  ```

## 5. Install Snap and Certbot for Let's Encrypt SSL
- **Install Snapd**:
  ```
  sudo apt update
  sudo apt install snapd
  ```
- **Enable Snapd Service**:
  ```
  sudo systemctl start snapd
  sudo systemctl enable snapd
  ```
- **Install Certbot**:
  ```
  sudo snap install --classic certbot
  ```

## 6. Obtain an SSL Certificate
- **Run Certbot for Nginx and follow the prompts**:
  ```
  sudo certbot --nginx
  ```
  Specify the domain for the certificate (e.g., `subdomain.yourdomain.com`).

## 7. Configure Nginx for SSL
- **Edit Nginx configuration file for your site**:
  ```
  sudo nano /etc/nginx/sites-available/subdomain.yourdomain.com.conf
  ```
- **Example configuration**:
  ```
  server {
      listen 443 ssl;
      server_name subdomain.yourdomain.com;

      ssl_certificate /etc/letsencrypt/live/subdomain.yourdomain.com/fullchain.pem;
      ssl_certificate_key /etc/letsencrypt/live/subdomain.yourdomain.com/privkey.pem;

      location /ws {
          proxy_pass http://localhost:9944;  # Forward requests to subtensor node
          proxy_http_version 1.1;
          proxy_set_header Upgrade $http_upgrade;
          proxy_set_header Connection "upgrade";
          proxy_set_header Host $host;
      }

      # Additional Nginx configuration...
  }
  ```
- **Enable the configuration**:
  ```
  sudo ln -s /etc/nginx/sites-available/subdomain.yourdomain.com.conf /etc/nginx/sites-enabled/
  ```

## 8. Verify and Reload Nginx
- **Test the configuration**:
  ```
  sudo nginx -t
  ```
- **Reload Nginx if the test is successful**:
  ```
  sudo systemctl reload nginx
  ```

## 9. Automated Renewal
- **Test the renewal process**:
  ```
  sudo certbot renew --dry-run
  ```
  Certbot usually sets up a cron job or systemd timer for automation.

## 10. Final Checks
- Verify that your site is accessible via HTTPS and that the SSL certificate is correctly installed.

**Note**: This is a general process for setting up an SSL certificate for a subdomain using Nginx and Let's Encrypt. Specific details may vary depending on server configuration and domain provider.