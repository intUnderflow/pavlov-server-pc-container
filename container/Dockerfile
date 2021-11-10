# It's worth noting you'll have to attach a game configuration yourself using container volume mounts or etc
# I've run this container inside containerd, your mileage with other CRIs may vary
FROM cm2network/steamcmd:steam

LABEL maintainer="pavlov-server-pc-container@lucy.sh"

# Install dependencies
RUN apt update && apt install -y gdb curl lib32gcc1 libc++-dev unzip

# Use steamcmd to download Pavlov Server
RUN /home/steam/steamcmd/steamcmd.sh +login anonymous +force_install_dir /home/steam/pavlovserver +app_update 622970 +exit

# Install latest steamclient.so file
RUN /home/steam/steamcmd/steamcmd.sh +login anonymous +app_update 1007 +quit
RUN mkdir -p ~/.steam/sdk64

RUN cp /home/steam/Steam/steamapps/common/Steamworks\ SDK\ Redist/linux64/steamclient.so  ~/.steam/sdk64/steamclient.so
RUN cp /home/steam/Steam/steamapps/common/Steamworks\ SDK\ Redist/linux64/steamclient.so ~/pavlovserver/Pavlov/Binaries/Linux/steamclient.so

# Create Log and Config Directories
RUN mkdir -p ~/pavlovserver/Pavlov/Saved/Logs
RUN mkdir -p ~/pavlovserver/Pavlov/Saved/Config/LinuxServer

# Make Pavlov server executable
RUN chmod +x ~/pavlovserver/PavlovServer.sh
