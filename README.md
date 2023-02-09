# Freedom Fighters Arma 3 Server Setup
This repo describes in detail how to setup a Arma 3 server and docker environment to support the Freedom Fighters community

Note: Remember to change the username and password in the steam command 

Note: this is note really needed, you can put it anywhere but if you go outside this guide you will need to edit all of the config files

Note: It is not a requirement for the steam user to have Arma 3 purchased but you will need a family sharing enabled if you use the User Interface to download Arma3


# Prepare the install
Download and install [steam](https://cdn.cloudflare.steamstatic.com/client/installer/SteamSetup.exe)

Download [steamcmd](https://steamcdn-a.akamaihd.net/client/installer/steamcmd.zip)

Unzip to `c:/steamcmd`

Download the files in this [repo](https://github.com/Nhimself/arma_server_setup/archive/refs/heads/main.zip) and unzip them - you will need them later

# Download and install Arma 3

Press `windowskey+R`

Write `run`

a command promt should open

Write `cd c:/steamcmd`

Write `steamcmd.exe +login steamUser password +force_install_dir C:\armaserver\arma +app_update 233780 validate +quit`

# Create folder structure

Create the following folder structure

Root folder

C:\armaserver 

 \arma\ <-- Arma install dir
 
 \arma\mpmissions\ <-- [Mission files](https://github.com/Nhimself/arma_server_setup/tree/main/mpmissions)
 
 \cfsync\ <-- [cfsync cli](https://github.com/Nhimself/arma_server_setup/tree/main/cfsync)
 
 \Config\ <-- [server config files](https://github.com/Nhimself/arma_server_setup/tree/main/Config)
 
 \mods\ <-- [server mods](https://cfo:snakes@repo-cfsync.charliefoxtrotops.com)
 
 \Profile\ <-- [Arma server profile](https://github.com/Nhimself/arma_server_setup/tree/main/Profile)




