FROM fedora:22

RUN dnf -y install dia

LABEL RUN "docker run -v \$HOME:\$HOME --net host -v /tmp/.X11-unix:/tmp/.X11-unix -e DISPLAY=\$DISPLAY -e XAUTHORITY=/.Xauthority -v ~/.Xauthority:/.Xauthority:ro vpavlin/dia

ENTRYPOINT dia
