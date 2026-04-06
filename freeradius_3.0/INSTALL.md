
1. Install FreeRADIUS server:
sudo apt update
sudo apt install -y freeradius freeradius-utils

2. Check RADIUS version:
freeradius -v

3. Check RADIUS server status：
sudo systemctl status freeradius

If NO RADIUS services：
sudo systemctl enable freeradius    # startup when OS boot
sudo systemctl start freeradius     # startup right now

4. 讓 FreeRADIUS server 的 LOGs 能夠在「前景」輸出，而非在「背景」執行：
sudo systemctl stop freeradius
sudo kill -s SIGTERM $(pidof "freeradius")
sudo freeradius -X &

5. Uninstall FreeRADIUS server:
# Remove free radius sever configurations
sudo apt purge freeradius-common freeradius-config -y

# Remove free radius sever binary files
sudo apt purge freeradius freeradius-utils -y            

sudo apt autoremove -y
sudo rm -rf /etc/freeradius
sudo rm -rf /var/log/freeradius

# Do check has any packages or not?
dpkg -l | grep freeradius

# Do check has any services or not?
systemctl status freeradius
Unit freeradius.service could not be found

#Do check has any ports or not?
ss -lunp | grep "1812 | 1813"
