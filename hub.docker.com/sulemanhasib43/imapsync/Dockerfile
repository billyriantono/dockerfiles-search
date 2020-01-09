FROM centos:7

WORKDIR /opt/app

RUN yum install -y epel-release && yum install -y imapsync wget

RUN yum install -y perl-App-cpanminus \
     perl-Dist-CheckConflicts \
     perl-HTML-Parser \
     perl-libwww-perl \
     perl-Module-Implementation \
     perl-Module-ScanDeps \
     perl-Package-Stash \
     perl-Package-Stash-XS \
     perl-PAR-Packer \
     perl-Regexp-Common \
     perl-Sys-MemInfo \
     perl-Test-Fatal \
     perl-Test-Mock-Guard \
     perl-Test-Requires \
     perl-Test-Deep \
     perl-File-Tail \
     perl-Unicode-String

RUN cpanm Encode::IMAPUTF7

RUN wget -N https://imapsync.lamiral.info/imapsync && chmod +x imapsync
RUN mv /usr/bin/imapsync /usr/bin/imapsync-old && cp ./imapsync /usr/bin/imapsync
