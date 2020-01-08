FROM ubuntu:17.10

LABEL maintainer="Per Junel <per.junel@gmail.com>"

# Replace 1000 with your user / group id
RUN export uid=1000 gid=1000 && \
     mkdir -p /home/developer && \
     echo "developer:x:${uid}:${gid}:Developer,,,:/home/developer:/bin/bash" >> /etc/passwd && \
     echo "developer:x:${uid}:" >> /etc/group && \
     chown ${uid}:${gid} -R /home/developer

WORKDIR /tmp/

USER developer

ENV HOME /home/developer

VOLUME /home/developer

CMD ["/bin/bash"]

# Run with
# docker run --net=host --env="DISPLAY" --volume="$HOME/.Xauthority:/root/.Xauthority:rw" -v $HOME:/home/developer/ --name ubuntu-user -it --rm peron/ubuntu-user:17.10

