FROM centos:6.8
#Prerequisites
RUN yum -y update
RUN yum -y install \ 
	redhat-lsb \
	libc.so.6 \
	libdl.so.2 \
	libpthread.so.0 \
	ld-linux.so.2 \
	zlib-devel-1.2.3-29.el6.x86_64 \
	zlib-1.2.3-29.el6.x86_64 \
	zlib-1.2.3-29.el6.i686
 

#Installing Nuance License Manager

ENV LICENSE_MANAGER_HOME /usr/local/Nuance/license_manager/
ENV LICENSE_MANAGER_SRC  /Nuance/Nuance_License_Manager/

COPY Nuance_License_Manager $LICENSE_MANAGER_SRC

WORKDIR $LICENSE_MANAGER_SRC
RUN ./install.sh default
COPY sdk-eval-recognizer10.lic $LICENSE_MANAGER_HOME/license/

WORKDIR $LICENSE_MANAGER_HOME
RUN  ./components/set-new-lic-file.sh \
	$PWD/license/sdk-eval-recognizer10.lic

RUN /etc/rc.d/init.d/nuance-licmgr restart

#Installing Nuance Recognizer

ENV RECOGNIZER_SRC  /Nuance/Nuance_Recognizer/
ENV RECOGNIZER_HOME /usr/local/Nuance/Recognizer/

COPY Nuance_Recognizer $RECOGNIZER_SRC

WORKDIR $RECOGNIZER_SRC
RUN ./install.sh default

#Installing languages
#English
env ENGLISH_LANG_SRC /Nuance/NRec-en-US-10.0.2-10.2.0/

COPY NRec-en-US-10.0.2-10.2.0 $ENGLISH_LANG_SRC
WORKDIR $ENGLISH_LANG_SRC

RUN ./install.sh default

#Spanish
env SPANISH_LANG_SRC /Nuance/NRec-es-ES-10.0.0-10.1.0/
COPY NRec-es-ES-10.0.0-10.1.0 $SPANISH_LANG_SRC
WORKDIR $SPANISH_LANG_SRC

RUN ./install.sh default

#Environment setup
COPY SETUP-env.sh /root/
COPY SETUP-env.sh /etc/profile.d/
COPY .bashrc /root/

ENV BASH_ENV=~/.bashrc
WORKDIR /WorkingDir

COPY /docker-run.sh /
ENTRYPOINT ["/docker-run.sh"]
