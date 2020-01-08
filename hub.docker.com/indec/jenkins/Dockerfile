FROM jenkins
MAINTAINER pablodgonzalez@gmail.com
USER root
RUN gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 && curl -sSL https://get.rvm.io | bash -s stable --with-gems="scss_lint,sass" --path /path/you/want/rvm/installed/to
USER jenkins