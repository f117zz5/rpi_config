# Mosquitto installation

```
sudo apt update
sudo apt install -y mosquitto mosquitto-clients
```

Make it autostart at boot:
```
sudo systemctl enable mosquitto.service
```

# Configuration

From link 3 below...


Add the lines bwllow to the config file:
```
per_listener_settings true
allow_anonymous false
password_file /etc/mosquitto/p2.txt
```
```
mosquitto_sub -u user -P pass -v -t '#'
```

# Links

1.  Quick Guide to The Mosquitto.conf File With Examples: [link](http://www.steves-internet-guide.com/mossquitto-conf-file/).
2. How to Install Mosquitto Broker on Raspberry Pi: [link](https://randomnerdtutorials.com/how-to-install-mosquitto-broker-on-raspberry-pi/).
3. Mosquitto Username and Password Authentication -Configuration and Testing [link](http://www.steves-internet-guide.com/mqtt-username-password-example/).

