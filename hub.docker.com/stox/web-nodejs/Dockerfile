FROM stox/nodejs

RUN sudo apt-get install -y curl git libfreetype6 libfontconfig

RUN curl -sSL https://rvm.io/mpapis.asc | gpg --import -
RUN curl -L https://get.rvm.io | bash -s stable

RUN /bin/bash -l -c 'export PATH=$PATH:/usr/local/rvm/bin >> .profile'
RUN /bin/bash -l -c 'echo "source /usr/local/rvm/scripts/rvm" >> .profile'

RUN /bin/bash -l -c "rvm requirements"

RUN /bin/bash -l -c "rvm install 2.1.2"
RUN /bin/bash -l -c "rvm use 2.1.2 --default"

RUN /bin/bash -l -c "gem install compass"
