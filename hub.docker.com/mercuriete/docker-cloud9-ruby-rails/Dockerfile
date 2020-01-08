FROM kdelfour/cloud9-docker

RUN gpg --keyserver hkp://pgp.mit.edu --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 || gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3
RUN curl -sSL https://get.rvm.io | bash -s stable --rails

#install tmux dependency that is needed for minitest
#install libpq-dev dependency to postgres gem
RUN apt-get install -y tmux libpq-dev

EXPOSE 8080
