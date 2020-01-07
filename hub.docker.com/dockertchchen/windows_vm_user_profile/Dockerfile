FROM dockertchchen/windows_vm:latest

RUN groupadd -g 1000 panchatcharama

RUN useradd -u 1000 -g 1000 -ms /bin/bash panchatcharama && echo "panchatcharama:panchatcharama" | chpasswd && adduser panchatcharama sudo

USER panchatcharama:panchatcharama

WORKDIR /home/panchatcharama