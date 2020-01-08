FROM debian:jessie
RUN apt-get update && \
    apt-get install -y git sudo libgd2-xpm-dev libgd-dev build-essential gcc g++ \
                       cmake curl libreadline-dev git-core libjpeg-dev libpng-dev \
                       ncurses-dev imagemagick unzip libqt4-dev liblua5.1-0-dev \
                       libgd-dev scons libgtk2.0-dev libsdl-dev
RUN git clone https://github.com/ehrenbrav/DeepQNetwork.git
RUN git config --global url.https://github.com/.insteadOf git://github.com/

RUN    cd DeepQNetwork && ./install_dependencies.sh 

