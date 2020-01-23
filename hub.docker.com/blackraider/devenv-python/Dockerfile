FROM blackraider/devenv-base 

MAINTAINER blackraider <er.blacky@gmail.com>

#RUN pacman-key --refresh-keys

USER root

RUN pacman -Syy --noconfirm
RUN pacman-db-upgrade

RUN pacman -S --noconfirm python python2 python-pip python2-pip python-virtualenv python2-virtualenv python-virtualenvwrapper 

USER developer

RUN mkdir -p /home/developer/projects/python
RUN mkdir -p /home/developer/projects/django

RUN mkdir -p /home/developer/.virtualenvs


RUN sed -i '$ a export WORKON_HOME=~/.virtualenvs' /home/developer/.bashrc
RUN sed -i '$ a source /usr/bin/virtualenvwrapper.sh' /home/developer/.bashrc
RUN sed -i '$ a export WORKON_HOME=~/.virtualenvs' /home/developer/.zshrc
RUN sed -i '$ a source /usr/bin/virtualenvwrapper.sh' /home/developer/.zshrc

USER root

RUN pip install request sqlalchemy twisted numpy ipython sqlobject pyinstaller py2exe django django-mysql
RUN pip2 install request sqlalchemy twisted numpy ipython sqlobject pyinstaller django django-mysql clientform pysqlite

USER developer

VOLUME /home/developer/projects/python
VOLUME /home/developer/projects/django

EXPOSE 8000 80 8080

