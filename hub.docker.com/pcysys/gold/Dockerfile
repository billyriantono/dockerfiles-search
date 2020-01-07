FROM linuxkonsult/kali-metasploit
MAINTAINER Automat-IT Team <ziv.kashtan@automat-it.com>

RUN export DEBIAN_FRONTEND=noninteractive
RUN apt-get install locales
RUN sed -i -e 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/' /etc/locale.gen && \
    locale-gen
ENV LANG en_US.UTF-8
RUN unset LANGUAGE
ENV LC_ALL C.UTF-8

#RUN dpkg-reconfigure locales
RUN locale
RUN echo "deb http://http.kali.org/kali kali-rolling main contrib non-free" > /etc/apt/sources.list
RUN echo "deb-src http://http.kali.org/kali kali-rolling main contrib non-free" >> /etc/apt/sources.list
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv ED444FF07D8D0BF6

WORKDIR /root
# RUN apt-get update --allow-unauthenticated && apt-get dist-upgrade -y --allow-unauthenticated && apt-get clean
RUN apt-get update
RUN apt-get install -y psmisc apache2 supervisor python-pip
RUN apt-get install -y nano vim openssh-server
RUN apt-get install -y apt-transport-https dirmngr
RUN pip install Crypto

RUN mkdir /var/run/sshd
RUN echo 'root:password' | chpasswd
RUN sed -i 's/PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN sed -i 's/#PermitRootLogin yes/PermitRootLogin yes/' /etc/ssh/sshd_config


# SSH login fix. Otherwise user is kicked off after login
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd

ENV NOTVISIBLE "in users profile"
RUN echo "export VISIBLE=now" >> /etc/profile

RUN sed -i 's/Listen 80/Listen 8090/' /etc/apache2/ports.conf

WORKDIR /root

RUN apt-get install -y scons
RUN dpkg --configure -a && apt-get install -y --allow-unauthenticated --upgrade metasploit-framework

RUN echo "deb https://download.mono-project.com/repo/debian stable-stretch main" | sudo tee /etc/apt/sources.list.d/mono-official-stable.list
RUN curl -s "https://keyserver.ubuntu.com/pks/lookup?op=get&search=0x3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF" | sudo apt-key add -

RUN apt-get update && apt-get install -y --allow-unauthenticated mono-complete mono-devel
RUN pip install pycrypto
RUN pip install pyscrypt
RUN pip install paramiko

RUN apt-get install -y mingw-w64
RUN wget -q https://cmake.org/files/v3.13/cmake-3.13.0-rc3-Linux-x86_64.sh -O /tmp/cmake-3.13.0-rc3-Linux-x86_64.sh && chmod +x /tmp/cmake-3.13.0-rc3-Linux-x86_64.sh
RUN /tmp/cmake-3.13.0-rc3-Linux-x86_64.sh --skip-license --prefix=/usr --exclude-subdir

COPY olympusFiles/* /var/www/html/

ADD hephaestus/ /root/hephaestus/
ADD hostrecon/ /root/hostrecon/
RUN rm -rf /root/hephaestus/.git* /root/hephaestus/bitbucket-pipelines.yml
RUN rm -rf /root/hostrecon/.git*
RUN rm -rf /root/hephaestus/Resources/vulcan/.git*

ADD boost_1_68_0 /root/hephaestus/Resources/vulcan/boost/
ADD openssl-1.1.1 /root/hephaestus/Resources/vulcan/openssl-1.1.1/
RUN cd /root/hephaestus/Resources/vulcan/openssl-1.1.1/ && ../mingw ./Configure mingw no-asm --prefix=/usr/i686-w64-mingw32/includes
RUN cd /root/hephaestus/Resources/vulcan/openssl-1.1.1/ && make && make install && make clean
RUN cd /root/hephaestus/Resources/vulcan/openssl-1.1.1/ && ../mingw64 ./Configure mingw64 no-asm --prefix=/usr/x86_64-w64-mingw32/includes
RUN cd /root/hephaestus/Resources/vulcan/openssl-1.1.1/ && make && make install
RUN rm -rf /root/hephaestus/Resources/vulcan/openssl-1.1.1/

COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf
RUN chmod +x *

COPY pcysys_run_commands.rb /usr/share/metasploit-framework/modules/post/multi/gather/

EXPOSE 22 55552
CMD ["/usr/bin/supervisord"]