FROM ubuntu:17.10

MAINTAINER kevenchen123@gmail.com

USER root

# ====== apt install ======

# used for ubuntu 14
#RUN curl http://archive.ubuntu.com/ubuntu/pool/universe/o/openjdk-8/openjdk-8-jre_8u45-b14-1_amd64.deb > /tmp/jre8.deb \
#    &&  curl http://archive.ubuntu.com/ubuntu/pool/universe/o/openjdk-8/openjdk-8-jre-headless_8u45-b14-1_amd64.deb > /tmp/jre.deb \
#    &&  curl http://archive.ubuntu.com/ubuntu/pool/universe/o/openjdk-8/openjdk-8-jdk_8u45-b14-1_amd64.deb > /tmp/jdk.deb \
#    &&  dpkg -i /tmp/jre.deb && dpkg -i /tmp/jre8.deb && dpkg -i /tmp/jdk.deb \
#    &&  rm /tmp/jre.deb && rm /tmp/jre8.deb && rm /tmp/jdk.deb

RUN apt-get update
RUN apt-get install openjdk-8-jdk -y

RUN apt-get install git-core gnupg flex bison gperf build-essential zip curl zlib1g-dev gcc-multilib g++-multilib libc6-dev-i386 lib32ncurses5-dev x11proto-core-dev libx11-dev lib32z-dev ccache libgl1-mesa-dev libxml2-utils xsltproc unzip python-networkx libssl-dev bc liblz4-tool rsync ruby subversion vim -y

# ====== change user ======

ENV MYNAME android
ENV MYPASS 123
ENV HOME /home/$MYNAME

RUN echo "User: $MYNAME Pass: $MYPASS Home: $HOME"
RUN useradd --create-home -d $HOME --shell /bin/bash --user-group --groups adm,sudo $MYNAME
RUN echo "$MYNAME:$MYPASS" | chpasswd

USER $MYNAME
WORKDIR $HOME

# ====== add ssh ======

RUN mkdir $HOME/tmp
RUN echo -e  'y\n' | ssh-keygen -q -t rsa -N "" -f ~/tmp/id_rsa

# ====== add repo ======

#RUN curl https://storage.googleapis.com/git-repo-downloads/repo > ~/repo
RUN echo "PATH=~/bin:$PATH" >> ~/.bashrc
COPY ./repo $HOME
USER root
RUN tar -xvf $HOME/repo.tar
RUN chmod 777 -R $HOME/bin && chmod 777 -R $HOME/repo

# ====== init config ======

CMD $HOME/bin/init.sh && su android  && /bin/bash
