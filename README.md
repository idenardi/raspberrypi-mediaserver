# Mediaserver
Media Server Script

## Install RDP
```
sudo apt-get purge realvnc-vnc-server
sudo apt-get install xrdp
sudo reboot
```

## HD/ Pendrive
#### Format
> https://cadernodelaboratorio.com.br/2017/10/30/hd-externo-com-o-raspberry-pi/
```
sudo umount /media/pi/sd32
sudo mkfs.ext4 /dev/sda1
sudo mkdir /media/pi/sd32
sudo mount /dev/sda1 /media/pi/sd32
sudo chown -R pi:pi /media/pi/sd32
sudo chmod 775 /media/pi/sd32
```
#### Auto mount
> https://pcmac.biz/raspberry-pi-mount-usb-drive.html
```
sudo blkid
sudo nano /etc/fstab
UUID=93ddc2e0-48e1-457c-9d59-f6a34596e6e1 /media/SSD-120GB ext4 defaults,nofail 0 0
sudo reboot
```
#### Clean cached
```
sudo apt autoremove
```
#### Remove folders
```
sudo rm -rf folderName
```
#### Change folders permissions
```
cd /media/pi
sudo chmod -R -v 777 *
```

## Docker:
#### Install some required packages first
```
sudo apt update
sudo apt install -y \
     apt-transport-https \
     ca-certificates \
     curl \
     gnupg2 \
     software-properties-common
```
#### Get the Docker signing key for packages
```
curl -fsSL https://download.docker.com/linux/$(. /etc/os-release; echo "$ID")/gpg | sudo apt-key add -
```
#### Add the Docker official repos
```
echo "deb [arch=armhf] https://download.docker.com/linux/$(. /etc/os-release; echo "$ID") \
     $(lsb_release -cs) stable" | \
    sudo tee /etc/apt/sources.list.d/docker.list
```
#### Install Docker
> The aufs package, part of the "recommended" packages, won't install on Buster just yet, because of missing pre-compiled kernel modules. We can work around that issue by using "--no-install-recommends"
```
sudo apt update
sudo apt install -y --no-install-recommends \
    docker-ce \
    cgroupfs-mount

sudo systemctl enable docker
sudo systemctl start docker
sudo usermod -aG docker pi
docker --version
```
## Docker compose
```
sudo apt update
sudo apt install -y python python-pip libffi-dev python-backports.ssl-match-hostname
sudo pip install docker-compose
docker-compose --version 
```
#### Run a docker compose file
```
docker-compose -f ~/docker/docker-compose.yml up -d
```

## Jacket 
- torrents (6): KickAssTorrent - MagnetDL - RARBG - The Pirate Bay - Torrentz2 - YTS
- http://192.168.0.117:9117/torznab/all

## Radarr Settings
- Media management movie naming
- Profiles
- Indexers (must no contains german, dutch, french, truefrench, danish, swedish, spanish, italian, korean, dubbed, swesub, korsub, dksubs, vain, HC, HDTS,)
- Indexers: http://192.168.0.117:9117/torznab/all
- Torrent client: 9001 admin/adminadmin (default password)

## Sonarr Settings
- Media management movie naming
- Profiles
- Indexers (must no contains german, dutch, french, truefrench, danish, swedish, spanish, italian, korean, dubbed, swesub, korsub, dksubs, vain, HC, HDTS,)
- Indexers: http://192.168.0.117:9117/torznab/all and anime categories (categories settings)
- Configurar torrent client: 9001 admin/adminadmin

## Plex Settings
- Add movies and tvshows folders
- Enable legends settings > agents > opensubitittle
