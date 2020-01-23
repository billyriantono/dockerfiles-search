FROM ubuntu:bionic

RUN apt update
RUN apt install -y software-properties-common sudo

RUN sudo apt install -y openssh-client openssh-server
RUN sudo apt install -y patch
RUN sudo apt install -y git
RUN sudo apt install -y curl
RUN sudo apt install -y libfontconfig
RUN sudo apt install -y libcurl4-openssl-dev

RUN sudo apt install -y libxml2-dev 
RUN sudo apt install -y libxslt1-dev 
RUN sudo apt install -y libqt4-dev
RUN sudo apt install -y memcached
RUN sudo apt install -y libsasl2-dev
RUN sudo apt install -y imagemagick
RUN sudo apt install -y libmagickcore-dev
RUN sudo apt install -y libmagickwand-dev 
RUN sudo apt install -y redis-server
RUN sudo apt install -y libqtwebkit-dev

RUN echo "mysql-server-5.7 mysql-server/root_password password password" | sudo debconf-set-selections
RUN echo "mysql-server-5.7 mysql-server/root_password_again password password" | sudo debconf-set-selections
RUN sudo apt install -y mysql-server
RUN sudo apt install -y libmysqlclient-dev 

RUN sudo apt-add-repository -y ppa:rael-gc/rvm
RUN sudo apt install -y rvm
RUN /bin/bash -l -c "rvm autolibs read-only"
RUN sudo apt install -y openssl1.0 libssl1.0-dev
RUN /bin/bash -l -c "rvm install 1.8.7"
RUN /bin/bash -l -c "gem update --system 1.8.25"
RUN /bin/bash -l -c "gem install bundler -v 1.10.6"
RUN echo "source /etc/profile.d/rvm.sh" >> /root/.bashrc

CMD /bin/bash
