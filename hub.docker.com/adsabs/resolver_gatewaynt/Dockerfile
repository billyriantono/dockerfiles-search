FROM adrianilloo/steam-runtime-i386

# Create Steam user for convenience on Steam apps (root user warning)
RUN adduser --disabled-password steam --gecos "Steam"

# Install main support software for building and testing HL2RP
ENV TERM xterm
ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update && echo 'Y' | apt-get dist-upgrade -y \
	&& apt-get install -fy curl git openssh-server screen && mkdir /var/run/sshd

# Add Steam user to sudoers, plus disable password prompt when using sudo
RUN adduser steam sudo \
	&& printf "\n# No root password prompt for Steam user\nsteam ALL=(ALL) NOPASSWD:ALL\n" >> /etc/sudoers

# SSH, SRCDS (main) ports
EXPOSE 22 27015

ENV HOME /home/steam
USER steam

# Download and install SteamCMD
WORKDIR $HOME/Steam/steamcmd
RUN sudo chown -R steam:steam . \
 	&& curl -sqL "https://steamcdn-a.akamaihd.net/client/installer/steamcmd_linux.tar.gz" \
	| tar zxvf - && ./steamcmd.sh +quit

# Install HL2DM and Source2013 servers. Copy helper executables.
WORKDIR	$HOME
COPY --chown=steam bin/* /usr/bin/
RUN sudo chown -R steam:steam . \
	&& sudo chmod -R +x /usr/bin \
	&& printf "\n. /usr/bin/.hl2rp-env\nsudo /usr/sbin/sshd\n" >> .bashrc \
	&& mkdir -p .steam/sdk32 \
	&& ln -s $HOME/Steam/steamcmd/linux32/steamclient.so .steam/sdk32/steamclient.so \
	&& sudo /usr/bin/update-hl2dm-server && sudo /usr/bin/update-source2013-server

# Fix missing library resolutions causing crashes on Source2013 server startup
WORKDIR $HOME/Steam/steamapps/common/source2013_server
RUN ln -s soundemittersystem_srv.so bin/soundemittersystem.so \
	&& ln -s scenefilecache_srv.so bin/scenefilecache.so

# Import Source2013 and HL2RP projects
WORKDIR $HOME/Projects
RUN sudo chown -R steam:steam . \
	&& git clone https://github.com/AdRiAnIlloO/SourceSDK2013 \
	&& git clone https://github.com/HL2RP/HL2RP

WORKDIR $HOME
