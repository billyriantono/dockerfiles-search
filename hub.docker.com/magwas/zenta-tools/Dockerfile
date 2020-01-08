FROM ubuntu:bionic

RUN apt-get update

RUN export DEBIAN_FRONTEND=noninteractive; apt-get -yy upgrade

RUN export DEBIAN_FRONTEND=noninteractive; apt-get -y install software-properties-common apt-transport-https locales

RUN apt-add-repository -y ppa:openjdk-r/ppa
RUN until apt-key adv --keyserver keys.gnupg.net --recv 43DB103F31060848; do echo retrying; done
RUN echo deb http://repos.demokracia.rulez.org/apt/debian/ unstable main >/etc/apt/sources.list.d/repos.demokracia.rulez.org.list

RUN apt-get update
RUN export DEBIAN_FRONTEND=noninteractive;apt-get -y install openjdk-8-jdk wget git xvfb unzip docbook-xsl make firefox tightvncserver dblatex libwebkitgtk-3.0-0 libswt-webkit-gtk-3-jni python-yaml python-pip python-dateutil zip debhelper devscripts zenta zenta-tools debhelper devscripts maven rsync


RUN useradd develop
RUN mkdir /home/develop
RUN chown develop:develop /home/develop

RUN mkdir /home/develop/lib; cd /home/develop/lib ; wget -q http://downloads.sourceforge.net/project/saxon/Saxon-HE/9.4/SaxonHE9-4-0-2J.zip;unzip SaxonHE9-4-0-2J.zip ; rm -f SaxonHE9-4-0-2J.zip

RUN mkdir /home/develop/build;cd /home/develop/build; git clone https://github.com/expath/xspec.git

RUN wget "http://search.maven.org/remotecontent?filepath=net/sourceforge/saxon/saxon/9.1.0.8/saxon-9.1.0.8.jar" -O /usr/local/lib/saxon9.jar

RUN pip install jira 

RUN ln -s /home/develop/lib /root/lib

RUN ln -s /home/develop/build /root/build

RUN git config --global user.email "mag+xsltbuilder@magwas.rulez.org"
RUN git config --global user.name "magwas/edemotest:xslt docker image"

RUN apt-get -y remove openjdk-7-jre openjdk-7-jre-headless openjdk-11-jre-headless
RUN git clone https://github.com/magwas/zenta-tools.git
RUN cd zenta-tools; ./bin/script
RUN rm -rf zenta-tools
CMD sudo su - develop



