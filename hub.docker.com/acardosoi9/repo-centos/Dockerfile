FROM debian:9.2

RUN apt-get update
RUN apt-get install -y wget dos2unix nginx openssh-server createrepo rpm tar gnupg sudo cron rsync
RUN apt-get upgrade -y 
RUN apt-get autoremove
RUN apt-get clean

# ENV ARCHITECTURE="x86_64"
ENV REPO_PASSWD="123456"
ENV REPO_ADDRESS="http://127.0.0.1"
ENV REPO_NAME="myrepo"
ENV GPG_NAME="John Doe"
ENV GPG_EMAIL="localhost@localhost"

ENV CENTOS_DIR="/etc/i9corp/packages/centos"

COPY ./tools/sync-repo /usr/local/bin/sync-repo
RUN dos2unix /usr/local/bin/sync-repo \
    && chmod +x /usr/local/bin/sync-repo

COPY ./tools/start-packages /usr/local/bin/start-packages
RUN dos2unix /usr/local/bin/start-packages \
    && chmod +x /usr/local/bin/start-packages

COPY ./tools/create-repo /usr/local/bin/create-repo
RUN dos2unix /usr/local/bin/create-repo \
    && chmod +x /usr/local/bin/create-repo

COPY ./tools/create-gpg /usr/local/bin/create-gpg
RUN dos2unix /usr/local/bin/create-gpg \
    && chmod +x /usr/local/bin/create-gpg

COPY ./nginx/centos /etc/nginx/sites-available/default

RUN mkdir -p ${CENTOS_DIR}/6.0/RPMS/x86_64
RUN mkdir -p ${CENTOS_DIR}/6.0/RPMS/i386
RUN mkdir -p ${CENTOS_DIR}/6.0/SRPMS/
RUN mkdir -p ${CENTOS_DIR}/5.11/RPMS/x86_64
RUN mkdir -p ${CENTOS_DIR}/5.11/RPMS/i386
RUN mkdir -p ${CENTOS_DIR}/5.11/SRPMS/

RUN /usr/local/bin/create-repo

RUN rsync -aqzH --exclude={'Cluster_Administration*','Deployment_Guide*','Global_File_System*','Virtualization*','gnome*','openoffice*'} archive.kernel.org::centos-vault/5.11/os/x86_64/CentOS/*.rpm /etc/i9corp/packages/centos/5.11/RPMS/x86_64/

RUN useradd -ms /bin/bash repo
RUN chown -R repo:repo /etc/i9corp/packages
RUN echo 'repo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

# CRON EM SILENT MODE 
# RUN echo "*/30 * * * * root /usr/bin/nohup sudo /usr/local/bin/sync-repo >/dev/null 2>&1 &" >> /usr/src/cron.tmp
# RUN echo "" >> /usr/src/cron.tmp \
#    && crontab /usr/src/cron.tmp \
#    && rm /usr/src/cron.tmp

WORKDIR /etc/i9corp/packages

RUN mkdir -p ~/.ssh \
    && touch ~/.ssh/authorized_keys \
    && chmod 644 ~/.ssh/authorized_keys

VOLUME [ "/etc/i9corp/packages" ]

#Nginx
EXPOSE 80

#SSH
EXPOSE 22

CMD ["/usr/local/bin/start-packages"]
