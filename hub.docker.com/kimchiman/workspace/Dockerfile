FROM ubuntu:16.04
MAINTAINER Luis <sskim.luis@gmail.com>

## Install SSH
RUN apt-get update && apt-get install -y openssh-server
RUN mkdir /var/run/sshd
RUN dpkg-reconfigure openssh-server
RUN sed -ri 's/^#?PermitRootLogin\s+.*/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN sed -ri 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config

RUN DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
apt-utils \
sudo \
locales \
gettext \
libgettextpo-dev \
tzdata \
vim \
curl \
wget \
git \
htop \
bash \
bash-completion \
net-tools \
dnsutils \
aptitude zsh \
python \
python-pip

## Set locale
RUN apt-get install -y language-pack-ko
RUN dpkg-reconfigure locales
RUN locale-gen ko_KR.UTF-8
RUN /usr/sbin/update-locale LANG=ko_KR.UTF-8
ENV LANG=ko_KR.UTF-8
ENV LANGUAGE=ko_KR.UTF-8
ENV LC_ALL=ko_KR.UTF-8

## Timezone
ENV TZ=Asia/Seoul
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

## Add user for luis
RUN useradd -m luis -s /bin/zsh && echo "luis:sangtn00" | chpasswd && adduser luis sudo

## Set nopassword permission to sudoer
RUN echo 'luis ALL=NOPASSWD: /usr/sbin/sshd' >> /etc/sudoers

## Install logcat-color
RUN pip install --upgrade pip
RUN git clone https://github.com/marshall/logcat-color.git && \
cd logcat-color; python setup.py install; cd ..; rm -rf logcat-color

## Prepare for Java download
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y python-software-properties
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y software-properties-common
RUN DEBIAN_FRONTEND=noninteractive add-apt-repository -y ppa:webupd8team/java
RUN DEBIAN_FRONTEND=noninteractive add-apt-repository -y ppa:openjdk-r/ppa
RUN DEBIAN_FRONTEND=noninteractive apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y \
default-jre \
default-jdk \
openjdk-7-jre \
openjdk-7-jdk

#grab oracle java (auto accept licence)
#RUN echo oracle-java7-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections
#RUN DEBIAN_FRONTEND=noninteractive apt-get install -y oracle-java6-installer oracle-java7-installer

## Set build environment for Android
RUN DEBIAN_FRONTEND=noninteractive sudo apt-get install -y \
git-core \
gnupg \
flex \
bison \
gperf \
build-essential \
zip \
curl \
zlib1g-dev \
gcc-multilib \
g++-multilib \
libc6-dev-i386 \
lib32ncurses5-dev \
x11proto-core-dev \
libx11-dev \
lib32z-dev \
ccache \
libgl1-mesa-dev \
libxml2-utils \
xsltproc \
unzip
RUN rm -rf /var/lib/apt/lists/*

## Install Oh-My-Zsh
USER luis
WORKDIR /home/luis
RUN mkdir /home/luis/.ssh
RUN wget https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh -O - | zsh || true
RUN sed -e s/robbyrussell/agnoster/g .zshrc > .zshrc.tmp
RUN mv .zshrc.tmp .zshrc

## Add a custom profile to .zshrc
RUN echo "" >> .zshrc
RUN echo "# Add custom bashrc" >> .zshrc
RUN echo "if [ -f ~/.bashrc_luis ]; then" >> .zshrc
RUN echo " . ~/.bashrc_luis" >> .zshrc
RUN echo "fi" >> .zshrc
COPY bashrc_luis /home/luis/.bashrc_luis

EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]
