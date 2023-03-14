## AutoCertbot
### What is AutoCertbot
* https://github.com/RomanRII/AutoCertbot
* This was developed to automate the needed steps to request a valid SSL certificate using certbot.
* Because HTTP inbound was needed, I opted to utilize Digital Ocean to generate the Droplet and manage the DNS record.
### What AutoCertbot Does
* It's pretty straight forward.
  * Create a Digital Ocean Droplet
  * Obtain it's IPv4 Address
  * Create the necessary firewall rules to allow HTTP inbound. Make sure to add the droplet in here
  * Run the commands to update the device, grab certbot, and request an SSL certificate using the provided parameters
  * Delete the droplet and created firewall
  * Output the fullchain.pem and privkey.pem into console for ez copy and paste
 
![image](https://user-images.githubusercontent.com/74742067/225129539-32e0f746-423d-4296-af7c-9c98a0d6d5bc.png)
