FROM ubuntu:14.04

RUN apt-get update && apt-get install qtcreator -y
RUN export uid=1000 gid=1000 && \
mkdir -p /home/developer && \
echo "developer:x:${uid}:${gid}:Developer,,,:/home/developer:/bin/bash" >> /etc/passwd && \
echo "developer:x:${uid}:" >> /etc/group && \
echo "developer ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/developer && \
chmod 0440 /etc/sudoers.d/developer && \
chown ${uid}:${gid} -R /home/developer

RUN apt-get install cmake -y

USER developer
ENV HOME /home/developer
RUN export QT_GRAPHICSSYSTEM="native"
CMD /usr/bin/qtcreator
