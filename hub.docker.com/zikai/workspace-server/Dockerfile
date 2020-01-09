FROM ubuntu:16.04

RUN apt-get -y update \
    && apt-get -y install wget rpm2cpio cpio \
           libgl1-mesa-glx libglib2.0-0 libxcomposite1 libxcursor1 \
           libxi6 libxtst6 libxss1 libfontconfig1 libxrandr2 libasound2 libegl1-mesa\
    && apt-get clean

RUN mkdir ~/workspace && cd ~/workspace \
    && wget -nv https://ws.data.csiro.au/collections/csiro:11028/data/4725691 \
    && mv 4725691 csiro.au-workspace-5.0.0-11780.x86_64.rpm \
    && rpm2cpio csiro.au-workspace-5.0.0-11780.x86_64.rpm | cpio -idmv

ADD WorkspaceServer.conf /root/.config/csiro.au/WorkspaceServer.conf
ADD ["Workspace Server.conf", "/root/.config/csiro.au/WorkspaceServer/Workspace Server.conf"]

EXPOSE 42151

CMD ["/root/workspace/opt/csiro.au/workspace/bin/workspace-server", "-e", "-platform", "minimal"]
