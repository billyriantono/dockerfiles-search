FROM kalilinux/kali-linux-docker:latest
MAINTAINER danilonc

# Update Kali
RUN apt-get update -y && apt-get dist-upgrade -y && apt-get autoremove -y

# Install Tools
RUN apt-get update -y && apt-get dist-upgrade -y && apt-get install metasploit-framework python-ipython tmux -y

# Start DB
RUN /etc/init.d/postgresql start && msfdb init && /etc/init.d/postgresql stop

# Default command
CMD /etc/init.d/postgresql start && bash -i
