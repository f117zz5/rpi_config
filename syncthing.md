# Installation

Follow the instructions [here](https://pimylifeup.com/raspberry-pi-syncthing/). Do not setup the remote access as this will be achieved using SSH port forwarding.
```
ssh -L 8080:127.0.0.1:8384 rpi3
```

Then open the browser on the laptop you are working and open `localhost:8080`. 