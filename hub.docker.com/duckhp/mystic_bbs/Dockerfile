# Mystic BBS (11.2 alpha41 based) Docker
# Please refer to http://wiki.mysticbbs.com for official Mystic BBS documentation.

#not using :latest, in hope to prevent version problems in the future
FROM alpine:3.9
#FROM alpine:latest
#frolvlad/alpine-glibc

MAINTAINER DuckHP <https://github.com/DuckHP>
LABEL maintainer="https://github.com/DuckHP" version="11.2 a41" description="Mystic BBS (11.2 alpha41 based) Docker \
Please see http://wiki.mysticbbs.com for official Mystic BBS documentation.\
Maintainer of this Dockerfile is NOT affiliated with Mystic BBS (http://mysticbbs.com/), or Cryptlib (https://www.cs.auckland.ac.nz/~pgut001/cryptlib/) author(s)."


########################
#
# Setup
#
########################

#required
ENV RUNTIME_REQUIRED_PACKS libc6-compat unrar unzip python2 py2-pip tmux curl busybox-suid
#ENV RUNTIME_REQUIRED_PACKS unrar unzip python2 py2-pip tmux curl busybox-suid

#useful archive/compression tools
ENV UTILS_ARCHIVE lzip bzip2 xz zip gzip tar lha unarj p7zip archivemount zlib

#optional tools
ENV UTILS_OPTIONAL nano neovim lynx dos2unix rsync clamav-scanner freshclam less

ENV BUILD_PACKS1="build-base linux-headers zlib-dev"
ENV BUILD_PACKS2="expect"
#might be nice to keep expect (needed to autoinstall mystic) and bash (needed to make dosemu(?)) around after cleanup

## MYSTIC BBS
# see:
# * http://mysticbbs.com
# * http://wiki.mysticbbs.com
ENV MYSTIC_DOWNLOAD_URL="https://archive.org/download/Mystic_BBS_v1.12_a41_linux/mys112a41_l64.rar" MYSTIC_X64_MD5_SIG=b351f4d9a0f835abbca3cebda5c3aef7
#ENV MYSTIC_DOWNLOAD_URL_X64 "http://mysticbbs.com/downloads/mys112a41_l64.rar"

## CRYPTLIB
# see:
# * http://wiki.mysticbbs.com/doku.php?id=cryptlib
# * https://www.cs.auckland.ac.nz/~pgut001/cryptlib
# * https://archive.org/details/cryptlib_cl3441
ENV CRYPTLIB_DOWNLOAD_URL="https://archive.org/download/cryptlib_cl3441/cl3441.zip" CRYPTLIB_MD5_SIG=f15918e6c8de373d59c0a08914d73369

## Expect/autoexpect script used to automate Mystic bbs install during build
# NOTE: It auto-selects options "2" , then changes install folders to "/home/mysticbbs/mystic/"
#
ENV AUTOEXPECT_SCRIPT_URL="https://raw.githubusercontent.com/DuckHP/mystic_bbs_docker/master/src/script_install.exp" AUTOEXPECT_SCRIPT_MD5_SIG=ab91ad0c5fbeb3d856dab998c591740f
#ENV AUTOEXPECT_SCRIPT_URL "https://pastebin.com/raw/wk0b4NDn"

## NO-IP (no-ip.com)
# set 'NOIP_BUILD 0' to exclude no-ip from the build
#
# for noip2 docs see:
# * http://www.no-ip.com
#
ENV NOIP_BUILD 1
ENV NOIP_DOWNLOAD_URL="https://archive.org/download/No-IP-2.1.9-1_linux/noip-duc-linux.tar.gz" NOIP_MD5_SIG=3b0f5f2ff8637c73ab337be403252a60

## INADYN (dyndns/freedns client)
# set 'INADYN_BUILD 0' to exclude inadyn from the build
# see:
# * https://help.dyn.com/inadyn/
# * freedns.afraid.org
# * dyndns.org
# * https://archive.org/details/inadyn_v1.96.2_src
#
ENV INADYN_BUILD 1
ENV INADYN_DOWNLOAD_URL="https://archive.org/download/inadyn_v1.96.2_src/inadyn.zip" INADYN_MD5_SIG=d394ed5ab7a9313992bdc62c412cb369
#ENV INADYN_DOWNLOAD_URL "http://cdn.dyndns.com/inadyn.zip"

## DropBear (ssh server)
# used to ssh into the docker container for remote admin the bbs backend
# see:
# * https://dropbear.nl/mirror/dropbear.html
#
ENV DROPBEAR_DOWNLOAD_URL="https://dropbear.nl/mirror/releases/dropbear-2018.76.tar.bz2"
ENV DROPBEAR_PORT 2222
ENV DROPBEAR_OPTIONAL dbclient dropbearconvert scp
ENV DROPBEAR_MD5_SIG c3912f7fcdcc57c99937e4a79480d2c2

## DOSEMU
#
# note: https://winworldpc.com/product/ms-dos/6x
ENV DOSEMU_BUILD 1
ENV DOSEMU_DOWNLOAD_URL="http://prdownloads.sourceforge.net/dosemu/dosemu-1.4.0-bin.tgz?download" DOSEMU_MD5_SIG=57e6589b735c5e878ddefbe513ec7efd
ENV DOSEMU_FREEDOS_DOWNLOAD_URL="http://prdownloads.sourceforge.net/dosemu/dosemu-freedos-1.0-bin.tgz?download" DOSEMU_FREEDOS_MD5_SIG=2e09774fe91cff4372cb4a393eb467f5


## Not in use YET. Intended to be used for potential autoconfiguration by 'mystic -cfg' + Expect script later
ENV MYSTIC_PORT_PREFIX=60 MYSTIC_TELNET_PORT=23 MYSTIC_SSH_PORT=22 MYSTIC_FTP_PORT=21
#ENV MYSTIC_WWW_PORT 80
#ENV MYSTIC_USER mysticbbs

########################
#
# Building
#
########################

## Alpine and python install
#
#
RUN	echo "STARTING BUILD!!" \
	&& apk update --progress \
	&& apk upgrade --progress \
	&& apk add --progress --no-cache ${RUNTIME_REQUIRED_PACKS} ${BUILD_PACKS1} ${BUILD_PACKS2} ${UTILS_ARCHIVE} ${UTILS_OPTIONAL} \
	&& pip install --no-cache-dir -U pip \
	&& wget -nc -O /tmp/python_requirements.txt "https://raw.githubusercontent.com/DuckHP/mystic_bbs_docker/master/src/requirements.txt" \
	&& pip install -r /tmp/python_requirements.txt \
	&& adduser -h /home/mysticbbs -D -s /bin/sh mysticbbs \
	&& su mysticbbs -c "mkdir -p /home/mysticbbs/.logs" \
	&& su mysticbbs -c "mkdir -p /home/mysticbbs/.config/supervisor-inc"


## download and checksum verification stage
#
#
RUN	cd /tmp/ \
	&& mkdir mystic && mkdir cryptlib \
	&& wget -nc -O /tmp/mystic/mystic.rar ${MYSTIC_DOWNLOAD_URL} \
	&& [[ "$(md5sum < /tmp/mystic/mystic.rar)" = "${MYSTIC_X64_MD5_SIG}  -" ]] && (echo "MD5 SUM CHECK OF 'mystic.rar' OK..") || (echo "MD5 SUM OF 'mystic.rar' INCORRECT! ABORTING!!";exit 1) \
	&& wget -nc -O /tmp/mystic/script_install.exp ${AUTOEXPECT_SCRIPT_URL} \
	&& [[ "$(md5sum < /tmp/mystic/script_install.exp)" = "${AUTOEXPECT_SCRIPT_MD5_SIG}  -" ]] && (echo "MD5 SUM CHECK OF 'script_install.exp' OK..") || (echo "MD5 SUM OF 'script_install.exp' INCORRECT! ABORTING!!";exit 1) \
	&& wget -nc -O /tmp/cryptlib/cryptlib.zip ${CRYPTLIB_DOWNLOAD_URL} \
	&& [[ "$(md5sum < /tmp/cryptlib/cryptlib.zip)" = "${CRYPTLIB_MD5_SIG}  -" ]] && (echo "MD5 SUM CHECK OF 'cryptlib.zip' OK..") || (echo "MD5 SUM OF 'cryptlib.zip' INCORRECT! ABORTING!!";exit 1)

## cryptlib build and install
#
# 	&& make shared >> /tmp/clbuild.log 2>&1 \
#
RUN	cd /tmp/cryptlib/ \
	&& unzip -a -q cryptlib.zip \
	&& echo "Building Cryptlib 'libcl.so' with 'make shared >> /tmp/clbuild.log 2>&1' ..Hold on to your pants!!" \
	&& make shared \
	&& export CRYPTLIB_BUILD_EXIT_CODE=$? \
	&& if [ ${CRYPTLIB_BUILD_EXIT_CODE} != 0 ]; then echo "Building Cryptlib failed!!\nBuild log below:\n" && cat /tmp/clbuild.log && exit ${CRYPTLIB_BUILD_EXIT_CODE} ;fi \
	&& echo "SUCCESS!! Building Cryptlib 'libcl.so' done! ..Installing 'libcl.so' into '/usr/lib/'" \
	&& mv libcl*.so* /usr/lib/libcl.so \
	&& unset CRYPTLIB_BUILD_EXIT_CODE

## mystic bbs install and backup
#
#
RUN	cd /tmp/mystic/ \
	&& unrar x mystic.rar \
	&& chmod +x ./script_install.exp \
	&& /usr/bin/expect -f ./script_install.exp \
	&& chown -R mysticbbs:mysticbbs /home/mysticbbs \
	&& su mysticbbs -c "touch /home/mysticbbs/.fresh && echo 0 > /home/mysticbbs/.fresh" \
	&& echo "Backing up the Mystic installation to ~/.mystic_install_$(date +'%Y-%m-%d').tar.gz .." \
	&& su mysticbbs -c "cd /home/mysticbbs && tar cfz ./.mystic_install_$(date +'%Y-%m-%d').tar.gz mystic" \
	&& echo "Backup created!"

## no-ip client step.
# see ENV NOIP_BUILD
#
RUN	if [ ! ${NOIP_BUILD} != 0 ] ; then echo "Skipping No-IP client build step!" ; else \
	echo "Adding No-IP client!!" \
	&& mkdir /tmp/noip \
	&& cd /tmp/noip \
	&& (wget -nc -O /tmp/noip/noip.tar.gz ${NOIP_DOWNLOAD_URL}) \
	&& [[ "$(md5sum < /tmp/noip/noip.tar.gz)" = "${NOIP_MD5_SIG}  -" ]] && (echo "MD5 SUM CHECK OF 'noip.tar.gz' OK..") || (echo "MD5 SUM OF 'noip.tar.gz' INCORRECT! ABORTING!!";exit 1) \
	&& tar -xzf /tmp/noip/noip.tar.gz -C /tmp/noip/ \
	&& cd /tmp/noip/noip-2.1.9-1/ \
	&& echo "Building 'noip2' ..Please wait..!" \
	&& make >> /tmp/noip2build.log 2>&1 \
	&& export NOIP_BUILD_EXIT_CODE=$? \
	&& if [ ${NOIP_BUILD_EXIT_CODE} != 0 ]; then echo "Building No-IP client failed!! Build log below:" && cat /tmp/noip2build.log && exit ${NOIP_BUILD_EXIT_CODE} ;fi \
	&& echo "Moving noip2 client binary to /usr/bin/noip2" \
	&& mv ./noip2 /usr/bin/ \
	&& unset NOIP_BUILD_EXIT_CODE \
	&& echo "No-IP client installed successfully!" ;fi

## inadyn dynamic dns client step
# see ENV INADYN_BUILD
#
RUN	if [ ! ${INADYN_BUILD} != 0 ] ; then echo "Skipping InaDyn client build step!" ; else \
	echo "Adding InaDyn client!!" \
	&& mkdir /tmp/inadyn \
	&& cd /tmp/inadyn \
	&& (wget -nc -O /tmp/inadyn/inadyn.zip ${INADYN_DOWNLOAD_URL}) \
	&& [[ "$(md5sum < /tmp/inadyn/inadyn.zip)" = "${INADYN_MD5_SIG}  -" ]] && (echo "MD5 SUM CHECK OF 'inadyn.zip' OK..") || (echo "MD5 SUM OF 'inadyn.zip' INCORRECT! ABORTING!!";exit 1) \
	&& unzip -a -q inadyn.zip \
	&& cd inadyn/ \
	&& echo "Building 'inadyn' ..Please wait..!" \
	&& make TARGET_ARCH=linux >> /tmp/inadynbuild.log 2>&1 \
	&& export INADYN_BUILD_EXIT_CODE=$? \
	&& if [ ${INADYN_BUILD_EXIT_CODE} != 0 ]; then echo "Building InaDyn client failed!! Build log below:" && cat /tmp/inadynbuild.log && exit ${INADYN_BUILD_EXIT_CODE} ;fi \
	&& echo "Moving inadyn client binary to /usr/bin/inadyn" \
	&& mv ./bin/linux/inadyn /usr/bin/inadyn \
	&& unset INADYN_BUILD_EXIT_CODE \
	&& echo "InaDyn $(/usr/bin/inadyn --version) installed sucessfully!" ;fi

## dropbear
#
#
RUN	mkdir /tmp/dropbear \
	&& cd /tmp/dropbear \
	&& wget -nc -O /tmp/dropbear/dropbear.tar.bz2 ${DROPBEAR_DOWNLOAD_URL} \
	&& [[ "$(md5sum <  dropbear.tar.bz2)" = "${DROPBEAR_MD5_SIG}  -" ]] && (echo "MD5 SUM CHECK OF 'dropbear.tar.bz2' OK..") || (echo "MD5 SUM OF 'dropbear.tar.bz2' INCORRECT! ABORTING!!";exit 1) \
	&& tar jxf dropbear.tar.bz2 \
	&& cd 'dropbear-2018.76/' \	
	&& ./configure \
	&& echo "Building Dropbear with 'make PROGRAMS=\"dropbear dropbearkey ${DROPBEAR_OPTIONAL}\" >> /tmp/dropbearbuild.log 2>&1'  ..Please wait..!" \
	&& make PROGRAMS="dropbear dropbearkey ${DROPBEAR_OPTIONAL}" >> /tmp/dropbearbuild.log 2>&1 \
	&& export DROPBEAR_BUILD_EXIT_CODE=$? \
	&& if [ ${DROPBEAR_BUILD_EXIT_CODE} != 0 ]; then echo "Building Dropbear failed!! Build log below:" && cat /tmp/dropbearbuild.log && exit ${DROPBEAR_BUILD_EXIT_CODE} ;fi \
	&& make install \
	&& echo "dropbear ssh server installed" \
	&& mkdir /etc/dropbear \
	&& chown -R mysticbbs:mysticbbs /etc/dropbear \
	&& chmod -R 700 /etc/dropbear \
	&& addgroup mysticbbs shadow \
	&& mkdir /home/mysticbbs/.ssh \
	&& touch /home/mysticbbs/.ssh/authorized_keys \
	&& touch /home/mysticbbs/.ssh/known_hosts \
	&& chown -R mysticbbs:mysticbbs /home/mysticbbs/.ssh

## DOSEMU
#
#
RUN	if [ ! ${DOSEMU_BUILD} != 0 ] ; then echo "Skipping dosemu build step!" ; else \
	echo "Adding DOSEMU + FreeDOS" \
	&& mkdir /tmp/dosemu \
	&& wget -O /tmp/dosemu/dosemu-1.4.0-bin.tgz ${DOSEMU_DOWNLOAD_URL} \
	&& [[ "$(md5sum < /tmp/dosemu/dosemu-1.4.0-bin.tgz)" = "${DOSEMU_MD5_SIG}  -" ]] && (echo "MD5 SUM CHECK OF 'dosemu.tgs' OK..") || (echo "MD5 SUM OF 'dosemu.tgz' INCORRECT! ABORTING!!";exit 1) \
	&& wget -O /tmp/dosemu/dosemu-freedos-bin.tgz ${DOSEMU_FREEDOS_DOWNLOAD_URL} \
	&& [[ "$(md5sum < /tmp/dosemu/dosemu-freedos-bin.tgz)" = "${DOSEMU_FREEDOS_MD5_SIG}  -" ]] && (echo "MD5 SUM CHECK OF 'dosemu-freedos-bin.tgz' OK..") || (echo "MD5 SUM OF 'dosemu-freedos-bin.tgz' INCORRECT! ABORTING!!";exit 1) \
	&& su mysticbbs -c "mkdir ~/.dosemu && mkdir ~/mydos" \
	&& su mysticbbs -c "cp /tmp/dosemu/dosemu-1.4.0-bin.tgz ~/mydos/" \
	&& su mysticbbs -c "cd ~/mydos/ && tar -zxf dosemu-1.4.0-bin.tgz" \
	&& su mysticbbs -c "cp /tmp/dosemu/dosemu-freedos-bin.tgz ~/mydos/" \
	&& su mysticbbs -c "cd ~/mydos/ && tar -zxf dosemu-freedos-bin.tgz" ;fi
##

#ADD --chown=mysticbbs:mysticbbs https://raw.githubusercontent.com/DuckHP/mystic_bbs_docker/master/src/ssh_login.sh /home/mysticbbs/.ssh_login.sh
COPY --chown=mysticbbs:mysticbbs ./src/ssh_login.sh /home/mysticbbs/.ssh_login.sh

RUN	chmod +x /home/mysticbbs/.ssh_login.sh


#copy/download the container boot script
COPY --chown=mysticbbs:mysticbbs ./src/boot.sh /.boot.sh
COPY --chown=mysticbbs:mysticbbs ./src/supervisord.conf /home/mysticbbs/.config/supervisord.conf
COPY --chown=mysticbbs:mysticbbs ./src/start.sh /home/mysticbbs/.start.sh
RUN	chmod +x /.boot.sh \
	&& chmod +x /home/mysticbbs/.start.sh

#set a random root passwd and default mystic passwd
USER root
RUN	echo "Setting random password for root user.." \
	&& passwd root -a sha512 -d $(head /dev/urandom | tr -dc A-Za-z0-9 | head -c 1025 ; echo '') \
	&& echo "Setting password to 'mystic' for 'mysticbbs' user ..Change it with 'passwd' later!" \
	&& passwd mysticbbs -a sha512 -d 'mystic' -u

#cleanup step
RUN	apk del --purge ${BUILD_PACKS1} \
	&& rm -rf /tmp/mystic \
	&& rm -rf /tmp/cryptlib \
	&& rm -rf /tmp/noip \
	&& rm -rf /tmp/inadyn

#tar needed files to use during populating volumes/mounts
USER root
COPY ./src/tar_files_list.txt /.tarlst.txt 
#ADD https://github.com/DuckHP/mystic_bbs_docker/blob/master/src/tar_files_list.txt /.tarlst.txt
RUN 	cd / \
	&& touch /.system.tar.gz \
	&& tar cvfa --remove-files '/.system.tar.gz' -T '/.tarlst.txt'

EXPOSE 23/tcp
EXPOSE 22/tcp
EXPOSE 2222/tcp
EXPOSE 2222/udp

ENTRYPOINT ["/.boot.sh"]

#snips below
#	&& if [ ${CRYPTLIB_BUILD_EXIT_CODE} != 0]; then exit 1 ;fi \
#
# 	&& su mysticbbs -c "touch /home/mysticbbs/.fresh"


