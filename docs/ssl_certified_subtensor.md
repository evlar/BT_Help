
# SSL Certificate Setup for a Subdomain Using Nginx

## 1. Setting Up a Subdomain and DNS 'A' Record
- **Purchase a Domain Name**:Setup a domain name with a domain registrar. There are many registrars available such as GoDaddy, Namecheap, and Google Domains.
- **Create a Subdomain**: Log into your domain management service (e.g., domain.com) and create a new subdomain (e.g., `node1.yourdomain.com`).
- **DNS 'A' Record**: Create a DNS 'A' record for the subdomain. Point this record to the IP address of your server.

## 2. Install Nginx on Your Server
- Update package lists:
  ```bash
  sudo apt update
  ```
- Install Nginx:
  ```bash
  sudo apt install nginx
  ```

## 3. Start and Enable Nginx
- Start Nginx service:
  ```bash
  sudo systemctl start nginx
  ```
- Enable Nginx to start on boot:
  ```bash
  sudo systemctl enable nginx
  ```

## 4. Firewall Adjustments
- Allow HTTP and HTTPS traffic:
  ```bash
  sudo ufw allow 'Nginx Full'
  sudo ufw reload
  ```
- Enable the firewall (if not already enabled):
  ```bash
  sudo ufw enable
  ```
- Allow SSH (to ensure remote access is not blocked):
  ```bash
  sudo ufw allow ssh
  ```

## 5. Install Certbot for Let's Encrypt SSL
- Install Certbot:
  ```bash
  sudo apt install certbot python3-certbot-nginx
  ```

## 6. Obtain an SSL Certificate
- Run Certbot for Nginx and follow the prompts:
  ```bash
  sudo certbot --nginx
  ```
- Specify the domain for the certificate (e.g., `subdomain.yourdomain.com`).

## 7. Configure Nginx for SSL
- Edit the Nginx configuration file for your site. Create one in `/etc/nginx/sites-available/` and link it in `/etc/nginx/sites-enabled/`.
- To create and edit this file, use:
  ```
  sudo nano /etc/nginx/sites-available/<subdomain.yourdomain.com>.conf
```
- Example configuration:
  ```nginx
  server {
      listen 443 ssl;
      server_name subdomain.yourdomain.com;

      ssl_certificate /etc/letsencrypt/live/subdomain.yourdomain.com/fullchain.pem;
      ssl_certificate_key /etc/letsencrypt/live/subdomain.yourdomain.com/privkey.pem;

      # Additional Nginx configuration...
  }
  ```
- Enable the configuration:
  ```bash
  sudo ln -s /etc/nginx/sites-available/subdomain.yourdomain.com /etc/nginx/sites-enabled/
  ```

## 8. Verify and Reload Nginx
- Test the configuration:
  ```bash
  sudo nginx -t
  ```
- Reload Nginx if the test is successful:
  ```bash
  sudo systemctl reload nginx
  ```

## 9. Automated Renewal
- Let's Encrypt certificates are valid for 90 days. Certbot can automatically renew them. Test the renewal process:
  ```bash
  sudo certbot renew --dry-run
  ```
- Certbot usually sets up a cron job or systemd timer for automation.

## 10. Final Checks
- Verify that your site is accessible via HTTPS and that the SSL certificate is correctly installed.

This is a general process for setting up an SSL certificate for a subdomain using Nginx and Let's Encrypt. Specific details may vary depending on server configuration and domain provider.