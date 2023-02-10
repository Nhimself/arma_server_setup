# Freedom Fighters Arma 3 Server Setup
This repo describes in detail how to setup a Arma 3 server and docker environment to support the Freedom Fighters community

A few notes before you begin
```
Remember to change the username and password in the steam command 

This is note really needed, you can put it anywhere but if you go outside this guide you will need to edit all of the config files

It is not a requirement for the steam user to have Arma 3 purchased but you will need a family sharing enabled if you use the User Interface to download Arma3
```

## 1. Prepare the install
Download and install [steam](https://cdn.cloudflare.steamstatic.com/client/installer/SteamSetup.exe)

Download [steamcmd](https://steamcdn-a.akamaihd.net/client/installer/steamcmd.zip)

Unzip to `c:/steamcmd`

Download the files in this [repo](https://github.com/Nhimself/arma_server_setup/archive/refs/heads/main.zip) and unzip them - you will need them later


## 2. Download and install Arma 3

Press `windowskey+R`

Write `run`

a command promt should open

Write `cd c:/steamcmd`

Write `steamcmd.exe +login steamUser password +force_install_dir C:\armaserver\arma +app_update 233780 validate +quit`


## 3. Create folder structure

Create the following folder structure

Root folder

C:\armaserver 

 \arma\ <-- Arma install dir
 
 \arma\mpmissions\ <-- [Mission files](https://github.com/Nhimself/arma_server_setup/tree/main/mpmissions)
 
 \cfsync\ <-- [cfsync cli](https://github.com/Nhimself/arma_server_setup/tree/main/cfsync)
 
 \Config\ <-- [server config files](https://github.com/Nhimself/arma_server_setup/tree/main/Config)
 
 \mods\ <-- [server mods](https://cfo:snakes@repo-cfsync.charliefoxtrotops.com)
 
 \Profile\ <-- [Arma server profile](https://github.com/Nhimself/arma_server_setup/tree/main/Profile)

## Run the server
[Download](https://github.com/Nhimself/arma_server_setup/blob/main/Run%20Primary%20Server.bat) to your desktop

To run the server you need to execute the `Run Primary Server.bat`


# CF sync infrastructure
CFsyn needs server infrastrcuture to run. This section describes how to setup this infrastructre using a docker environment. If you are only looking for the setup of an addtional server, you can **skip** this section. 

### A few observations and facts:
```
- CFsync uses a caddy file server to list and download the mod files, it is not an explicit requirement to use caddy, but the files needs to be served in raw form. 
- CFsync uses a file called modlist.cfm to maintain which mods the server and the client should start with 
- modlist.cfm also works as a config file that allows for the cfsync client to display the servers avaliable
- CFsync uses a file has to map each file and locate an updated version
- There is a currently known bug that not all mods is synced with the client, even if the client claims to need an updated version
```


## Infrastructure description

1. A server to maintain a list of mod files and a modlist.cfm config file
2. A server to host the squad.xml file
3. A server to host the cfsync files and config setup
 - This repo contains a series of important files
 - config.csm for 

### config.csm
The config.csm file contain information for the client

1. Basepath for location of the mods
2. RepositoryURL for the repository location of the mods
3. UpdatesURL where the updated mods are located
4. ModlistFile which files to download and update

The file looks like this:
```
{
    "BasePath":"c:\\CFMods",
    "RepositoryURL": "https://cfo:snakes@repo-cfsync.charliefoxtrotops.com",
    "UpdatesURL": "https://cfo:snakes@cfsync.charliefoxtrotops.com",
    "ModlistFile":"modList.cfm"
}
```

### version.csm
The version.csm file contains information wheter the cfsync client has been updated. 



## Docker compose file
This section contains a description of the docker compose file and what is needed, the assumption is that you already have docker desktop installed and know how to oprate a docker environment. 

There are several methods to run a docker environment and opinions on maintaining this. This is a representation of how I run it and you may choose your own path. 

There are 4 volumes mounted into the caddy file.
- the [caddy file](https://github.com/Nhimself/cfsync_web/blob/master/Caddyfile)
- the mods to run the server
- the squad xml
- the cfsync lib

This method lets you serve all three webservers from one caddy instance. If you expect high loads on your mods repo I would suggest seperating it to a server with more resources. 



```
version: "3.7"

services:
  caddy:
    image: caddy:latest
    #restart: unless-stopped
    ports:
      - "80:80" 
      - "443:443"
    volumes:
      - 'C:\Caddyfile:/etc/caddy/Caddyfile'
      - 'C:\armaserver\mods:/var/www/modsrepo/'
      - 'C:\squad\:/var/www/squad/'
      - 'C:\armaserver\arma\cfsync:/var/www/cfsync/'
    restart: unless-stopped
```



