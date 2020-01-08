FROM codercom/code-server:latest

USER coder

RUN mkdir -p /home/coder/.local/share/code-server/extensions

WORKDIR /home/coder/project

RUN sudo apt-get update && sudo apt-get -y install python-pip
RUN sudo pip install -U PlatformIO

VOLUME ["/home/coder/.local/share/code-server"]

ENTRYPOINT ["dumb-init", "code-server", "--host", "0.0.0.0", "--auth", "none"]


