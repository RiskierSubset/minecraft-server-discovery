# minecraft-server-discovery
Tool to discover minecraft servers on the internet all over the world and visualize them on a website.

## SETUP
- [Setup using docker (easiest)](#docker)
- [Setup frontend (no docker)](#frontend)
- [Setup backend (no docker)](#backend)

Website example: 
![image](https://user-images.githubusercontent.com/14212955/172442508-b72047e5-18b6-4932-9b73-94073c8d0cb7.png)
Scanner example:
![image](https://user-images.githubusercontent.com/14212955/172442759-df75ffd9-8986-448c-8cfb-1ac2398d7997.png)

All data fields saved in database:
- IP address
- Port
- Messsage of the day (motd) (message visible when viewing server in server browser)
- Minecraft server version (including modded)
- Current amount of players
- Max amount of players
- Latency (from API location to minecraft server)
- First discovered date
- Last seen online date
- Sample of players (currently not working)
- Continent of server
- Country of server
- Region name of server
- Zipcode of server
- Latitude of server
- Longitude of server
- Isp of server
- Timezone of server

## Frontend
The frontend is written in Angular and is very basic with basic functionality. It has the option to refresh the data of a specific server and open the geo-location of the server on Google Maps. You are able to click on the 'players' header to sort based on active players.
To run the front-end, just install NPM, install packages (npm install) and serve the website (ng serve)

## Backend
The backend is split up in two different projects; the scanner and the API.

The scanner is setup to be easy to use. It guides the user through a couple of questions to setup the scanner. Once the setup is done, it will start scanning all the given IP ranges.
When the scanner finds an IP with port 25565 open, it will send a GET request to the API. To run the scanner on the whole internet, use IP range "0.0.0.0/0".
To run the scanner, simply build the project and execute the exe

The API tries to connect to the Minecraft server, and extracts as much info as possible from the server. The server and geo-location get saved in a Database.
To run the API, simply build the project and execute the exe. Make sure to have the environment variable "MINECRAFT_DISCOVERY_DB" set on your machine and have the value be a valid connection string to a MySQL database.

## Docker
- Clone the repository (or pull the new version)
- Open terminal in root of the repository
- Compose the containers (the backend should crash a couple of times, this is because it takes like ~20 seconds to setup the DB container. Just give it some time, it restarts automatically)
  - Execute `docker-compose up`  (you can remove everything with `docker-compose down -v` and remove the images) OR 
  - Execute `sudo docker compose build --no-cache && sudo docker compose up --force-recreate` (you can remove everything with `sudo docker compose down -v` and remove the images)
- Everything should be running (frontend: `localhost:80`, backend: `localhost:5000`)
- You can now start the Wrapper on your machine (same machine as you just ran these commands on

## TODO
- [ ] Change the SUBMIT endpoint to a messagebus so it's all more efficient
- [ ] Add more functionality to front-end, like filters
- [ ] Detect OS in scanner and point to non-exe file when it's not Windows
- [ ] Detect if NpCap (or something similar) is installed
- [ ] Fix the player list (as of right now, the players are not received. This should be fixed in the package that is used
- [ ] Add more default lists
- [ ] Add the ability to pass arguments to the Wrapper
- [X] Add docker container with all of the stuff setup
- [X] Make .NET versions consistent


## Credits
SieBRUM

https://github.com/robertdavidgraham/masscan

https://github.com/FragLand/minestat
