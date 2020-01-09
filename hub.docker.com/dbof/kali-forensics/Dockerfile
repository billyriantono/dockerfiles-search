FROM kalilinux/kali-linux-docker
MAINTAINER Davide Bove <me@davidebove.com>

### apt-get install kali-linux-forensic 
RUN apt-get -y update \
    && apt-get install -y sleuthkit \
        autopsy \
        # testdisk also contains photorec
        testdisk \
        foremost \
        scalpel \ 
        less \
        hexer \
        sqlite3 \
        man \
        libimage-exiftool-perl perl-doc \
    && apt-get clean

# install fiwalk, which contains idifference.py
RUN wget http://digitalcorpora.org/downloads/fiwalk/fiwalk_version.txt -q \
    && wget http://digitalcorpora.org/downloads/fiwalk/$(cat fiwalk_version.txt) \
    && tar -xf $(cat fiwalk_version.txt) -C /opt && rm $(cat fiwalk_version.txt) fiwalk_version.txt \
    && mkdir /home/forensics

WORKDIR /home/forensics
CMD ['/bin/bash']
