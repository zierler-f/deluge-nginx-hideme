# Prerequisites
## Installed programs
In order to start the stack the following programs will need to be installed on the machine:
* Docker (please refer to https://docs.docker.com/engine/installation/ for installation details)
* Docker Compose (please refer to https://docs.docker.com/compose/install/ for installation details)

## Account at hide.me
Besides Docker and Docker Compose the only other thing needed to run the stack is an account at http://hide.me/ (you can register at https://hide.me/en/pricing)

# Installation
## Download from Github
Once the prerequisites are fulfilled, clone this repository by opening a shell, navigate to a location of your choosing and type:
```shell
git clone git@github.com:zierler-f/deluge-nginx-hideme.git
```
## Change file to work with your setup
Now navigate into the cloned folder and open the file called 'docker-compose.yml' with the text editor of your choice and make the following changes:
* Find the line `- <local-folder>:/downloads` (under services -> deluge -> volumes) and replace `<local-folder>` with the download destination of your choosing on your local machine.
* At the bottom of the file replace `<hide.me-username>` with your username from http://hide.me/ and `<hide.me-password>` with the corresponding password.

## Run the stack
Once you changed the file accordingly, save the changes, and close the file. Now go back to your shell and open the project folder again. Now you can start Deluge, OpenVPN and Nginx at the same time by typing:
```shell
docker-compose up -d
```
Once the command is finished all containers should be up and running, and most importantly, the deluge-container should have a different IP than your local machine.
## Access Deluge
There are two ways to access deluge, once the programs are up and running:
* The WebUI is available under `http://<host-ip>:8112`. The default password is `deluge`.
* To access Deluge from the deluge-gtk add a connection to `<host-ip>` at port `58846`. Both username and password for the connection are `deluge`.

## Compare IPs
To make sure the IP is set correctly, and different to your hosts IP first go to http://ipecho.net and memorize the IP, or write it down. Next, download the file at http://checkmytorrentip.net/torrentip/checkMyTorrentIp.png.torrent and add it to deluge. Under the status of the added torrent, you can see the public IP of the container. If the IP is different to the IP you saw earlier, you are good to go. If the IPs are the same, however, make sure the `<hide.me-username>` and `<hide.me-password>` variables are set correctly in 'docker-compose.yml'.

# Stop stack
To stop the stack, go back into the folder where `docker-compose.yml` is located and type:
```shell
docker-compose stop
```
to start it again, type:
```shell
docker-compose start
```

# Remove stack
To completely remove the stack, and everything it created, type:
```shell
docker-compose down
```
