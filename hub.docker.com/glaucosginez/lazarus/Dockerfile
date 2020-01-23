FROM ubuntu:18.04

RUN apt-get update && apt-get upgrade -y

RUN apt-get install -y

RUN apt-get install -y wget binutils gcc gdb \
    libgtk2.0-0 libgtk2.0-dev \
    libcanberra-gtk-module \
    libgl1

RUN wget https://ufpr.dl.sourceforge.net/project/lazarus/Lazarus%20Linux%20amd64%20DEB/Lazarus%202.0.0/fpc-laz_3.0.4-1_amd64.deb

RUN wget https://ufpr.dl.sourceforge.net/project/lazarus/Lazarus%20Linux%20amd64%20DEB/Lazarus%202.0.0/fpc-src_3.0.4-2_amd64.deb

RUN wget https://ufpr.dl.sourceforge.net/project/lazarus/Lazarus%20Linux%20amd64%20DEB/Lazarus%202.0.2/lazarus-project_2.0.2-0_amd64.deb

RUN dpkg -i fpc*.deb

RUN dpkg -i lazarus*.deb

RUN wget https://deb.nodesource.com/setup_10.x \
    && chmod +x setup_10.x \
    && ./setup_10.x \
    && apt-get install -y nodejs

RUN rm *.deb

RUN rm setup_10.x

RUN apt-get clean && apt-get autoremove -y
