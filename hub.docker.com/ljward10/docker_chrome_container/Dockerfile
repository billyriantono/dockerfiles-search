# Firefox over VNC on Ubuntu 15.10

FROM ubuntu:15.10

RUN apt-get update && apt-get install -y firefox sudo

RUN apt-get install -y libxss1 libappindicator1 libindicator7 wget
RUN wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
RUN apt-get install -y gconf-service libgconf-2-4 libnspr4 libnss3 libpango1.0-0 fonts-liberation libcurl3 xdg-utils
RUN dpkg -i google-chrome*.deb

#Add new sudo user
ENV USERNAME lance
RUN useradd -m $USERNAME && \
        echo "$USERNAME:$USERNAME" | chpasswd && \
        usermod --shell /bin/bash $USERNAME && \
        usermod -aG sudo $USERNAME && \
        echo "$USERNAME ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers.d/$USERNAME && \
        chmod 0440 /etc/sudoers.d/$USERNAME && \
        # Replace 1000 with your user/group id
        usermod  --uid 1000 $USERNAME && \
        groupmod --gid 1000 $USERNAME
