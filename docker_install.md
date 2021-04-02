## Installing Docker
I used this guide [here](https://phoenixnap.com/kb/docker-on-raspberry-pi). The installation script:
```
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
```
Now adding a non-root user to the docker group
```
sudo usermod -aG docker [user_name]
```

## Installing pihole using Docker
Starting from [this](https://fictionbecomesfact.com/2019/03/17/installing-docker-pi-hole-image-with-dhcp-server/) article
```
sudo docker pull pihole/pihole

```


After starting pihole with the script, get a random password:
```
docker logs pihole 2> /dev/null | grep 'password:'
```
To change the password of pihole, original article [here](https://www.reddit.com/r/Ubiquiti/comments/dvik8g/persistent_pihole_via_docker_on_udmpro/):
```
docker exec -it pihole /bin/bash
```

# Starting things

## portainer
```
sudo docker run -d -p 9000:9000 -p 8000:8000 --name portainer --restart always -v /var/run/docker.sock:/var/run/docker.sock -v /home/iangelov/docker/portainer_data:/data portainer/portainer
```

## OpenwebRX

see this article: https://github.com/jketterl/openwebrx/wiki/Getting-Started-using-Docker
