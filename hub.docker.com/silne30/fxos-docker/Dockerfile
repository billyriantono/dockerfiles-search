FROM dorowu/ubuntu-desktop-lxde-vnc

MAINTAINER John Dorlus <jdorlus@mozilla.com>

RUN rm /bin/sh && ln -s /bin/bash /bin/sh

RUN dpkg --add-architecture  i386

RUN apt-get update 

RUN apt-get install -y --no-install-recommends autoconf2.13 bison bzip2 ccache curl flex gawk gcc g++ g++-multilib gcc-4.7 g++-4.7 g++-4.7-multilib git lib32ncurses5-dev lib32z1-dev libgconf2-dev zlib1g:amd64 zlib1g-dev:amd64 zlib1g:i386 zlib1g-dev:i386 libgl1-mesa-dev libx11-dev make zip libxml2-utils  lzop

RUN update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-4.7 1 && \
    update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-4.8 2 && \
    update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-4.7 1 && \
    update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-4.8 2 && \
    update-alternatives --set gcc "/usr/bin/gcc-4.7" && \
    update-alternatives --set g++ "/usr/bin/g++-4.7" 

RUN apt-get install -y python2.7

RUN python2.7 -V

RUN apt-get install -y python-setuptools

RUN easy_install pip

RUN pip install virtualenv virtualenvwrapper

RUN mkdir -p /opt/virtualenvs

ENV WORKON_HOME /opt/virtualenvs

RUN /bin/bash -c "source /usr/local/bin/virtualenvwrapper.sh \
    && mkvirtualenv gaia-workspace \
    && workon gaia-workspace \
    && pip install pytest" 


RUN apt-get install -y nodejs

RUN apt-get install -y git

RUN echo "source /usr/local/bin/virtualenvwrapper.sh" >> /etc/bash.bashrc

RUN mkdir /home/gaia-env && chmod 777 /home/gaia-env &&  cd /home/gaia-env &&  git clone git://github.com/mozilla-b2g/gaia

RUN apt-get install -y wget libgtk2.0-0:i386 libidn11:i386 libglu1-mesa:i386 libpangox-1.0-0:i386 libpangoxft-1.0-0:i386

RUN apt-get install -y libasound2 libxt6

RUN ln -s /usr/bin/nodejs /usr/bin/node

RUN apt-get install -y vim

RUN apt-get install -y xvfb

RUN curl -L https://npmjs.org/install.sh | sh

RUN cd /home/gaia-env/gaia/tests/python/gaia-ui-tests && python setup.py develop


RUN chmod 777 -R /home/gaia-env/
