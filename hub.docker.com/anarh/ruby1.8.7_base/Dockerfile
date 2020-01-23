FROM anarh/h_centos6.6

RUN yum update -y &&  \
    yum install -y \
      yum-plugin-ovl \
      graphviz \
      ImageMagick \
      ImageMagick-devel; yum clean all

#run the rest as a non-root account
#it's a hack to make the uid fixed at 1000 due to virtualbox bind-mount permissions
RUN useradd -u 1000 -ms /bin/bash railsapp
RUN echo "railsapp ALL=(ALL) NOPASSWD:ALL" > /etc/sudoers
USER railsapp

RUN command curl -sSL https://rvm.io/mpapis.asc | gpg2 --import -
RUN curl -sSL https://get.rvm.io | bash -s master
RUN /bin/bash -l -c "rvm requirements && rvm install 1.8.7 && rvm install ree-1.8.7-2012.02 && rvm cleanup all"
RUN /bin/bash -l -c "rvm use --default ree-1.8.7-2012.02"
RUN /bin/bash -c -l "echo 'gem: --no-ri --no-rdoc' > ~/.gemrc"
RUN /bin/bash -l -c "gem update --system 1.8.26"
