FROM peron/ubuntu-user

MAINTAINER peron <per.junel@gmail.com>

RUN sudo apt-get update && \
    sudo apt-get install -y \
      firefox

ENTRYPOINT ["firefox"]

# Build with: docker build -t ubuntu-firefox .
# Run with: docker run -ti --rm -e DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix:ro ubuntu-firefox
# Source for GUI related stuff:
#    http://fabiorehm.com/blog/2014/09/11/running-gui-apps-with-docker/
