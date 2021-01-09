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
```



