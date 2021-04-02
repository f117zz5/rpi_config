# Getting the RPi ready

## Prepare the server
First generate a new server key, do not use the default one. Link to the article [here](https://www.kali.org/docs/arm/kali-linux-raspberry-pi/):
```
root@kali:~ rm /etc/ssh/ssh_host_*
root@kali:~ dpkg-reconfigure openssh-server
root@kali:~ service ssh restart
```


## Generating a key pair

From this article [here](https://help.github.com/en/github/authenticating-to-github/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)
```
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```
Where -C adds a description, it could be something like "Laptop1".

## Copy the pub key to the remote server
From this article [here](https://www.simplified.guide/ssh/copy-public-key)
```
ssh-copy-id -i ~/.ssh/other_key.pub user@remote-host
```

## Convert OpenSSH keyf for Android
From this article [here](https://creodias.eu/-/how-to-convert-linux-openssh-key-to-putty-format-)
```
puttygen id_rsa -o id_rsa.ppk
```
Under Android ConnectBot and TotalCommander require PEM format. Here how to convert the files, original article [here](https://unix.stackexchange.com/questions/26924/how-do-i-convert-a-ssh-keygen-public-key-into-a-format-that-openssl-pem-read-bio)
```
ssh-keygen -f id_rsa.pub -e -m pem > id_rsa.pem
```
## Test password of a private SSH key
The password can be tested like
```
ssh-keygen -f id_rsa -y
```
this will read the private key and print the public key to the stdout. 

## Enable pub key auth only

Using this article here: [link](https://medium.com/@Imesha94/enabling-public-key-ssh-authentication-on-your-vps-fe5bfbf94822)

```
RSAAuthentication yes
PubkeyAuthentication yes
AuthorizedKeysFile .ssh/authorized_keys
```
Note: I do not find RSAAuthentication in my RPI3 sshd_config file.

On the Buster Lite it was not working, so I needed to add the newly generated key to may ssh agent by using:
```
ssh-add ~/.ssh/rpi3/id_rsa
```

Also here is an example of my ssh config file
```
host rpi3
  Hostname 192.168.0.100
  User pi
  IdentityFile ~/.ssh/rpi3
```