FROM mayeut/centos-buildpacks:centos5-curl

ADD mercurial.selenic.com.repo /etc/yum.repos.d/

# procps is very common in build systems, and is a reasonably small package
RUN yum -y update \
 && yum -y install epel-release.noarch \
 && yum -y install \
    bzr.x86_64 \
    git.x86_64 \
    mercurial.x86_64 \
    openssh-clients.x86_64 \
    subversion.x86_64 \
    procps.x86_64 \
 && find /usr/lib/locale/ -mindepth 1 -maxdepth 1 -type d -not -path '*en_US*' -exec rm -rf {} \; \
 && find /usr/share/locale/ -mindepth 1 -maxdepth 1 -type d -not -path '*en_US*' -exec rm -rf {} \; \
 && localedef --list-archive | grep -v -i ^en | xargs localedef --delete-from-archive \
 && mv /usr/lib/locale/locale-archive  /usr/lib/locale/locale-archive.tmpl \
 && /usr/sbin/build-locale-archive \
 && echo "" >/usr/lib/locale/locale-archive.tmpl \
 && find /usr/share/{man,doc,info} -type f -delete \
 && rm -rf /etc/ld.so.cache \
 && rm -rf /var/cache/ldconfig/*
	
