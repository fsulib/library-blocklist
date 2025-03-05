Pi-Hole dnsmasq

Setting up a dnsmasq server on a Raspberry Pi is relatively simple. Here’s a step-by-step guide to get you started:

**1. Update Your Raspberry Pi**   
Before beginning, ensure your Raspberry Pi is up-to-date. Run the following commands in the terminal:
bash
Copy
**sudo apt update**
**sudo apt upgrade**
**sudo apt dist-upgrade**
**sudo reboot**

**2. Install dnsmasq**
Install dnsmasq using the following command:
bash
Copy
**sudo apt install dnsmasq**

**3. Backup Default Configuration**
Before modifying the configuration, it's always a good idea to back up the original file:
bash
Copy
**sudo cp /etc/dnsmasq.conf /etc/dnsmasq.conf.backup**

**4. Configure dnsmasq**

Now, you’ll need to edit the dnsmasq configuration file to suit your needs.
bash
Copy

**sudo nano /etc/dnsmasq.conf**

Here are some common settings you might want to modify:

• Set DNS server: If you want your Raspberry Pi to act as a DNS server, add the following line to configure it to forward DNS queries to an upstream DNS provider (e.g., Google's DNS servers).

bash
Copy

**server=8.8.8.8**

*Or, use a different DNS provider such as Cloudflare’s* **1.1.1.1.**

• Configure DHCP range: If you want dnsmasq to handle DHCP (assigning IP addresses to devices on your network), you can set a DHCP range. Add these lines to the file:

bash
Copy

**interface=eth0    #** or **wlan0 for wireless, specify your interface**
**dhcp-range=192.168.1.100,192.168.1.200,12h**

This gives out IP addresses between **192.168.1.100** and **192.168.1.200,** with a lease time of 12 hours.
• Set a static IP for your Raspberry Pi (optional but useful if you need your Pi to always have the same IP). If you're using the Pi as a DHCP server, add a line like this to assign a fixed IP address to the Pi:

bash
Copy
**dhcp-host=XX:XX:XX:XX:XX:XX,192.168.1.50**

Replace XX:XX:XX:XX:XX:XX with your Raspberry Pi’s MAC address.

**5. Restart dnsmasq**

Once you’ve made your changes, save the file **(press CTRL+X, then Y, then Enter to save and exit).** Restart dnsmasq to apply the changes:
bash
Copy
**sudo systemctl restart dnsmasq**

**6. Enable dnsmasq to Start on Boot**

Ensure that dnsmasq starts automatically whenever the Raspberry Pi reboots:
bash
Copy
**sudo systemctl enable dnsmasq**

**7. Check the Status**

You can check if dnsmasq is running properly by running:
bash
Copy
**sudo systemctl status dnsmasq**
If everything is configured correctly, you should see an active status.

**8. Test the DNS Server**

To check if the DNS server is working, you can try pinging a domain name from another device on the network or directly from the Raspberry Pi itself:
bash
Copy
**ping google.com**
If you get a response, the DNS server is working correctly.

**9. (Optional) Configure Firewall (if necessary)**

If you have a firewall on your Raspberry Pi (e.g., ufw), ensure the necessary ports are open for DNS and DHCP:
bash
Copy
**sudo ufw allow 53  # DNS port**
**sudo ufw allow 67  # DHCP port**

**10. (Optional) Set Up Additional Features**
 
DNS Caching: dnsmasq caches DNS queries, so requests should resolve faster.
• DNS for Local Devices: You can configure dnsmasq to resolve local device names, making it easier to connect to devices without needing to remember IP addresses.
• Advanced DHCP Configuration: You can customize DHCP options such as DNS servers, gateway, etc., using **dhcp-option** in the **dnsmasq.conf file.**
Conclusion
Once these steps are completed, your Raspberry Pi will act as a DNS and DHCP server. You can further customize it by adjusting the settings **in /etc/dnsmasq.conf** based on your network requirements.


