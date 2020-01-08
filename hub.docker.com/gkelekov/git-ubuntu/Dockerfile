# Base system is the latest LTS version of Ubuntu.
from   ubuntu


# Make sure we don't get notifications we can't answer during building.
env    DEBIAN_FRONTEND noninteractive


# Prepare scripts and configs
add    ./scripts/start.sh /start.sh


# Download and install everything from the repos.
run    apt-get -q -y update; apt-get -q -y upgrade && \
       apt-get -q -y install sudo openssh-server && \
       apt-get -q -y install sudo git && \
       mkdir /var/run/sshd


# Set root password
run    echo 'root:password' >> /root/passwdfile


# Create user and it's password
run    useradd -m -G sudo master && \
       echo 'master:password' >> /root/passwdfile


# Apply root password
run    chpasswd -c SHA512 < /root/passwdfile && \
       rm /root/passwdfile


# Port 22 is used for ssh
expose 22


# Assign /data as static volume.
volume ["/data"]


# Fix all permissions
run    chmod +x /start.sh


# Starting sshd
cmd    ["/start.sh"]
