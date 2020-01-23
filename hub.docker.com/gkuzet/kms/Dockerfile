FROM ubuntu
MAINTAINER Gordon Kuzet "gordon@kuzet.com"
# Install required packages
RUN ["sh", "-c", "apt-get update && apt-get install -y \
wget \
unzip \
build-essential \
man-db \
"]
# Download KMS server from 3rd party GitHub as zip archive and unzip
RUN ["sh", "-c", "wget https://github.com/Wind4/vlmcsd/archive/master.zip"]
RUN ["sh", "-c", "unzip master.zip"]
# Go into unzipped folder and compile the binaries and copy into /usr/local/bin
WORKDIR /vlmcsd-master
RUN ["sh", "-c", "make"]
WORKDIR /vlmcsd-master/bin
RUN ["sh", "-c", "cp * /usr/local/bin"]
# Install man pages (create man folders for custom man pages (non package), copy from unzipped archive and update mandb index)
WORKDIR /usr/local/share/man
RUN ["sh", "-c", "mkdir man1 man7 man8"]
WORKDIR /vlmcsd-master/man
RUN ["sh", "-c", "cp vlmcs.1 /usr/local/share/man/man1/"]
RUN ["sh", "-c", "cp vlmcsd.7 /usr/local/share/man/man7/"]
RUN ["sh", "-c", "cp vlmcsd.8 /usr/local/share/man/man8/"]
RUN ["sh", "-c", "mandb"]
# Cleanup (remove unzippd archive and zip archive downloaded
WORKDIR /
RUN ["sh", "-c", "rm -rf /vlmcsd-master"]
RUN ["sh", "-c", "rm master.zip"]
# Designate the start entry and options
ENTRYPOINT ["/usr/local/bin/vlmcsd", "-D"]
CMD ["-l", "/var/log/vlmcsd.log"]
# open relevant KMS service port
EXPOSE 1688