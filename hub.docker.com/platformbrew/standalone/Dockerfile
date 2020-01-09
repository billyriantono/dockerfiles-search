FROM sjackman/linuxbrew-standalone

# TODO: Query @sjackman about following lines - they shouldn't be
# nessecary - is linuxbrew-standalone the wrong thing to target?
USER root
RUN mkdir /.cache && chown -R linuxbrew:linuxbrew /.cache && apt-get install -y unzip

# platform-brew needs Python, but linuxbrew's Python doesn't work
# (cannot write to /Library).
RUN apt-get install -y python

USER linuxbrew

RUN brew update && brew tap platform-brew/tap && brew install platform-brew
