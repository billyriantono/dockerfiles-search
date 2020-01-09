FROM leeruniek/teamcity-agent
USER root

RUN apt-get update
RUN apt-get install nodejs postgresql build-essential patch ruby-dev zlib1g-dev \
 		liblzma-dev qt5-default libqt5webkit5-dev git sudo libssl-dev libreadline-dev \
 		gstreamer1.0-plugins-base gstreamer1.0-tools gstreamer1.0-x libffi-dev libpq-dev -y

RUN gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 && \curl -sSL https://get.rvm.io | bash -s stable
RUN echo source /usr/local/rvm/scripts/rvm >> /root/.bashrc
RUN bash -l rvm install 2.3.0

# RUN source /home/teamcity/.rvm/scripts/rvm && rvm install 2.3.0



