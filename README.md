# Multistream-WSL-Ubuntu-Stunnel4-Nginx-OBS-Win10

Multistreaming at home or own server using Latest Ubuntu 20 LTS or WSL (Windows Sub Linux) Windows 10

### Requirements
1. Windows 10 (latest update)
2. Ubuntu 20 LTS (WSL)
3. Stunnel 4 (for facebook rtmps)
4. OBS (or prefferred stream app)


### Installing Ubuntu20 LTS
1. Go to Microsoft Store and search for Ubuntu20
2. Choose Ubuntu 20 LTS and Install
3. Restart your computer
4. Enabling WSL2 (optional)
5. Visit [LINK](https://docs.microsoft.com/en-us/windows/wsl/install-win10 "Microsoft Guide")

or 
Press Windows then type in: "Powershell" right click on it then "Run as Administrator"
paste the code below:
```
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
```
then paste the other one:
```
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```

6. Open Ubuntu 20 LTS and type your prefferred username and password
7. Update the System type in: (this will take a moment)
```
sudo apt update
sudo apt upgrade
```

### Installing NGINX and RTMP MOD
```
sudo apt-get install nginx
sudo apt install libnginx-mod-rtmp
```

### Allowing NGINX interface
```
sudo ufw allow 'Nginx HTTP'
```

### NGINX commands
```
sudo systemctl stop nginx.service
sudo systemctl start nginx.service
sudo systemctl enable nginx.service

sudo service nginx start
{start|stop|restart|reload|force-reload|status|configtest|rotate|upgrade}
```

### NGINX Configuration
#### NOTE: Replace this with your {stream_key};
```
sudo nano /etc/nginx/nginx.conf

rtmp_auto_push on;

rtmp {
  server {
    listen 1935;
    chunk_size 4096;

    application live {
      live on;
      record off;

      #RTMP EXAMPLES
      #Facebook (Stunnel) RTMPS
      push rtmp://127.0.0.1:19350/rtmp/{stream_key};
      #Facebook (Deprecated)
      push rtmp://rtmp-pc.facebook.com:80/rtmp/{stream_key};
      #Twitch
      push rtmp://live-sea.twitch.tv/app/{stream_key};
      #Youtube
      push rtmp://x.rtmp.youtube.com/live2/{stream_key};
    }
  }
}
```

### Installing Stunnel4
```
sudo apt install stunnel4
```

### Config Stunnel4
#### 1.)
```
sudo nano /etc/stunnel/stunnel.conf
```
#### Type in:
```
setuid = stunnel4
setgid = stunnel4
pid=/tmp/stunnel.pid
output = /var/log/stunnel4/stunnel.log
include = /etc/stunnel/conf.d
```

#### 2.) Change Enable=0 to:
```
sudo nano /etc/default/stunnel4

ENABLE=1
```

#### 3.) Create other configs
```
sudo mkdir /etc/stunnel/conf.d
cd /etc/stunnel/conf.d/
sudo touch fb.conf
sudo nano fb.conf
```

#### 4.) Type in:
```
[fb-live]
client = yes
accept = 127.0.0.1:19350
connect = live-api-s.facebook.com:443
verifyChain = no
```

#### Stunnel Commands
```
sudo service stunnel4 start
sudo service stunnel4 stop
sudo service stunnel4 restart
```

##### Note: Whenever you edit the nginx.conf save it and reload without restarting nginx type in:
```
sudo service nginx reload
```


### Run OBS and change settings go to Stream tab
```
Service: custom 
Server: rtmp://<server ip>/live
Stream Key: <streamkey of your choice>
```

### To get ubuntu20 IP address open its console and type in:
```
sudo apt install net-tools

ifconfig -a

find eth0 (most cases)
```

### Day to day startup
```
sudo /etc/init.d/stunnel4 start
sudo /etc/init.d/nginx start 
ifconfig -a
```

### Enjoy Streaming!



