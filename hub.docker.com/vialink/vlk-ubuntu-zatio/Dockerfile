FROM vialink/vlk-ubuntu
ARG DEBIAN_FRONTEND=noninteractive

LABEL version="1.0"
LABEL author="Mauricio Nunes <mnunes@vialink.com.br>"

RUN apt-get update && apt install -y rng-tools git make mysql-client \
    build-essential python-dev solr-jetty gawk\
    cups cups-bsd apache2 libapache2-mod-wsgi lynx \
    python-setuptools libjpeg-dev libfreetype6 \
    libfreetype6-dev zlib1g-dev openjdk-8-jdk libssl-dev \
    libffi-dev lsb-core autossh unzip python-pip && \
    apt-get autoremove && apt-get clean

RUN chsh -s $(which zsh)

RUN /bin/zsh --login -c "/bin/zsh ~/.zshrc" 

ENTRYPOINT [ "/bin/zsh" ]
