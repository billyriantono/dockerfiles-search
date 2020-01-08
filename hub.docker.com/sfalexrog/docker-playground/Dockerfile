FROM ubuntu:16.04

RUN useradd -d /home/user -ms /bin/bash -g root -G sudo user

USER user
WORKDIR /home/user

CMD ["/bin/bash"]

