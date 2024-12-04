# 🚀 OpenLiteSpeed Installation on Ubuntu Server  

## 📖 Overview  
OpenLiteSpeed is a lightweight, open-source, and high-performance web server. This guide walks you through the installation and basic configuration of OpenLiteSpeed on an Ubuntu Server running in VirtualBox.

---

## 🛠️ Features  
- Easy-to-use web-based admin panel.  
- Built-in support for PHP and multiple PHP versions.  
- High performance and lightweight design.  
- Free and open-source.  

---

## 🖥️ Requirements  
1. **Ubuntu Server** (20.04/22.04 or later).  
2. **VirtualBox** with a configured virtual machine.  
3. Internet connectivity.  
4. Basic knowledge of Linux commands.

---

## ⚙️ Installation Steps  

### Step 1: Update and Prepare the System  
Ensure your system is up to date:
```bash
sudo apt update && sudo apt upgrade -y
sudo apt install wget curl -y
```

### Step 2: Add OpenLiteSpeed Repository  
Run the following command to add the OpenLiteSpeed repository:
```bash
wget -O - https://repo.litespeed.sh | sudo bash
```

### Step 3: Install OpenLiteSpeed  
Install OpenLiteSpeed:
```bash
sudo apt install openlitespeed -y
```
Start and enable the OpenLiteSpeed service:
```bash
sudo systemctl enable lsws
sudo systemctl start lsws
```

### Step 4: Access Admin Panel  
- Open a browser and navigate to: `http://<IP_SERVER>:7080`.  
- Default credentials:  
  - **Username:** `admin`  
  - **Password:** `123456`  

💡 You’ll be prompted to change the password after logging in.  

### Step 5: Configure PHP Support  
Install PHP 8.1:
```bash
sudo apt install lsphp81 lsphp81-common lsphp81-mysql -y
```
Connect PHP to OpenLiteSpeed via the admin panel:
1. Go to **Server Configuration > External App**.  
2. Add an external app for PHP with these details:  
   - **Name:** `lsphp81`  
   - **Address:** `uds://tmp/lshttpd/lsphp.sock`.  

Restart OpenLiteSpeed via the admin panel to apply changes.  

### Step 6: Test Your Setup  
Create a test PHP file:
```bash
sudo nano /usr/local/lsws/Example/html/info.php
```
Add the following code:  
```php
<?php
phpinfo();
?>
```  
Access it in your browser:  
`http://<IP_SERVER>/info.php`

---

## 🔥 Firewall Configuration  
Ensure ports are open to allow access:  
```bash
sudo ufw allow 7080/tcp
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp
sudo ufw reload
```

---

## 📝 Post-Installation Tasks  
1. Secure the admin panel by changing the default password:  
   ```bash
   sudo /usr/local/lsws/admin/misc/admpass.sh
   ```  
2. Set up your website or applications by uploading files to:  
   `/usr/local/lsws/Example/html`.

---

## 🎉 You're Ready to Go!  
Your OpenLiteSpeed server is now up and running! Start hosting your web applications with a lightweight and high-performance server.  
 
