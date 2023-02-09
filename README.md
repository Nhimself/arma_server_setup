# arma_server_setup
This repo describes in detail how to setup a Arma 3 server and docker environment to support the Freedom Fighters community

Note: Remember to change the username and password on line 20
Note: this is note really needed, you can put it anywhere but if you go outside this guide you will need to edit all of the config files 


# Prepare the install
Download and install steam https://cdn.cloudflare.steamstatic.com/client/installer/SteamSetup.exe

Download and unzip steamcmd https://steamcdn-a.akamaihd.net/client/installer/steamcmd.zip to c:/steamcmd


# Download and install Arrma 3
Press windowskey+R
Enter run
a command promt should open
Enter cd c:/steamcmd

Enter steamcmd.exe +login steamUser password +force_install_dir C:\armaserver\arma +app_update 233780 validate +quit


#Prepare windows
create the following folder structure

Root folder
c:\armaserver 

\arma\ <-- Arma install dir
\arma\mpmissions\ <-- custom mission files goes here!!!!
\cfsync\ <-- cfsync cli to run the server with 
\Config\ <-- server config dir
\mods\ <-- server mods dir
\Profile\ <-- Arma server profile dir




