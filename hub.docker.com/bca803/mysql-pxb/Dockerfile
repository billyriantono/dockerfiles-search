## MySQL 5.6 with Percona Xtrabackup
 
## Pull the mysql:5.6 image
FROM mysql:5.6
 
## The maintainer name and email
MAINTAINER Ashraf Sharif <ashraf@s9s.com>
 
## List all packages that we want to install
ENV PACKAGE percona-xtrabackup-24
 
# Install requirement (wget)
RUN apt-get update && apt-get install -y wget
 
# Install Percona apt repository and Percona Xtrabackup
RUN wget https://repo.percona.com/apt/percona-release_0.1-4.jessie_all.deb && \
    dpkg -i percona-release_0.1-4.jessie_all.deb && \
    apt-get update && \
    apt-get install -y $PACKAGE
 
# Create the backup destination
RUN mkdir -p /backup/xtrabackups

# Copy the script to simplify backup command
ADD run_backup.sh /run_backup.sh
 
# Allow mountable backup path
VOLUME ["/backup/xtrabackup"]
