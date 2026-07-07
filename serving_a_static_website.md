This project demonstrates how to host a static website using Nginx as a web server. It includes HTML, CSS, and JavaScript files, along with instructions for configuring a custom domain.
steps to set up the project:
## Features

- Static website hosting with Nginx
- Custom domain configuration
- HTML, CSS, and JavaScript assets
- Easy deployment on Ubuntu
- access the website via HTTPS using Let's Encrypt.
## Project Structure

```
.
├── css/
├── js/
├── images/
├── index.html
└── README.md
```

# Installation
### 1. Install Nginx on your server by:
   - On Ubuntu/Debian: `sudo apt update && sudo apt install nginx`

---

### 2. Clone the Repository

Clone this repository to your server.

```bash
git clone https://github.com/omar-mazen/weatherio.git 
```

Move into the project directory.

```bash
cd weatherio
```

---

### 3. prepare the website files by creating a directory for your domain and setting the appropriate permissions:
```
sudo mkdir -p /var/www/yourdomain.com/html 
sudo chown -R $USER:$USER /var/www/yourdomain.com/html
```

### 4. copy the project files to the `/var/www/yourdomain.com/html` directory.

### 5. configure nginx by creating a new configuration file for your domain:

```
sudo nano /etc/nginx/sites-available/yourdomain.com
```
copy the following configuration into the file:

```
server {
    listen 80;
    server_name yourdomain.com;

    root /var/www/yourdomain.com/html;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }
}
```

### 6. enable the configuration by creating a symbolic link to the `sites-enabled` directory:

``` 
sudo ln -s /etc/nginx/sites-available/yourdomain.com /etc/nginx/sites-enabled/
```

### 7. test and reload Nginx configuration by running:
``` 
sudo nginx -t
sudo systemctl reload nginx
```

### 8. Set up a domain name and point it to your server's IP address.   

### 9. Restart Nginx to apply the changes.
### 10. Access your website by navigating to `http://yourdomain.com` in a web browser.  
### 13. (Optional) Set up SSL for your domain using Let's Encrypt for secure HTTPS access using certbot:
### 14. Obtain a domain name using any free domain name provider like Freenom or use a paid domain name from providers like Namecheap, GoDaddy, etc.

``` 
sudo apt install certbot python3-certbot-nginx
sudo certbot --nginx -d yourdomain.com -d www.yourdomain.com

```
now your website should be accessible via HTTPS.
