# install-chrome-browser-linux
Cara install browser chrome di linux NON-GUI

**Install Docker**
```
apt update -y && sudo apt upgrade -y
```
```
for pkg in docker.io docker-doc docker-compose podman-docker containerd runc; do sudo apt-get remove $pkg; done
```
```
sudo apt-get install ca-certificates curl gnupg
```
```
sudo install -m 0755 -d /etc/apt/keyrings
```
```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```
```
sudo chmod a+r /etc/apt/keyrings/docker.gpg
```
```
echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```
```
sudo apt update -y && sudo apt upgrade -y
```
```
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

**Cek Zona Waktu**
```
realpath --relative-to /usr/share/zoneinfo /etc/localtime
```

#<h1>**Install Chrome**</h1>
**1. Buat Folder Untuk Chrome**
```
mkdir chromium
cd chromium
```

**2. Buat File docker-compose.yaml**
```
nano docker-compose.yaml
```

**3. Paste kode dibawah ini**
```
services:
  chromium:
    image: lscr.io/linuxserver/chromium:latest
    container_name: chromium
    security_opt:
      - seccomp:unconfined #optional
    environment:
      - CUSTOM_USER=User-Name     #Ganit User-Name
      - PASSWORD=Password    #Ganti Password
      - PUID=1000
      - PGID=1000
      - TZ=Europe/London
      - CHROME_CLI=https://google.com #optional
    volumes:
      - /root/chromium/config:/config
    ports:
      - 3010:3000   #Ganti 3010 ke port favoritmu
      - 3011:3001   #Ganti 3011 ke port favoritmu
    shm_size: "1gb"
    restart: unless-stopped
```

#<h1>Menjalankan Chrome</h1>
```
cd $HOME && cd chromium
docker compose up -d
```

**Sekarang kamu bisa akses browser chrome di pc lokal-mu**
> IP-server:port-yang-kamu-buat
