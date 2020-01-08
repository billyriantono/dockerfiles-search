# =========================================================================
# =========================================================================
#
#	Dockerfile
#	  Dockerfile for Kaptain 0.73-2 in a Debian docker container.
#
# =========================================================================
#
# @author Jay Wheeler.
# @version 9.6.1-gtk3
# @copyright © 2017, 2018. EarthWalk Software.
# @license Licensed under the GNU General Public License, GPL-3.0-or-later.
# @package ewsdocker/debian-kaptain
# @subpackage Dockerfile
#
# =========================================================================
#
#	Copyright © 2017, 2018. EarthWalk Software
#	Licensed under the GNU General Public License, GPL-3.0-or-later.
#
#   This file is part of ewsdocker/debian-kaptain.
#
#   ewsdocker/debian-kaptain is free software: you can redistribute 
#   it and/or modify it under the terms of the GNU General Public License 
#   as published by the Free Software Foundation, either version 3 of the 
#   License, or (at your option) any later version.
#
#   ewsdocker/debian-kaptain is distributed in the hope that it will 
#   be useful, but WITHOUT ANY WARRANTY; without even the implied warranty 
#   of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
#   GNU General Public License for more details.
#
#   You should have received a copy of the GNU General Public License
#   along with ewsdocker/debian-kaptain.  If not, see 
#   <http://www.gnu.org/licenses/>.
#
# =========================================================================
# =========================================================================
FROM ewsdocker/debian-base-gui:9.6.0-gtk3

MAINTAINER Jay Wheeler <EarthWalkSoftware@gmail.com>

ENV DEBIAN_FRONTEND=noninteractive

# ==============================================================================
# ==============================================================================
#
# https://github.com/mviereck/kaptain/raw/master/kaptain_0.73-2_amd64_debian.deb
#
# ==============================================================================
# ==============================================================================

# =========================================================================
#
#   ARG_SOURCE <== url of the local source (http://alpine-nginx-pkgcache), 
#                   otherwise external source.
#
#       Build option:
#         --build-arg ARG_SOURCE=http://alpine-nginx-pkgcache --network=pkgnet
#
# =========================================================================

ARG ARG_SOURCE

ENV PKG_HOST=${ARG_SOURCE:-"https://github.com/mviereck/kaptain/raw/master"}

ENV PKG_NAME=kaptain_0.73-2_amd64_debian.deb
ENV PKG_DIR=kaptain
ENV PKG_URL=${PKG_HOST}/${PKG_NAME}

# =========================================================================

ENV LMSBUILD_VERSION="9.6.1-gtk3"
ENV LMSBUILD_NAME=debian-kaptain 
ENV LMSBUILD_REPO=ewsdocker
ENV LMSBUILD_REGISTRY=""

ENV LMSBUILD_PARENT="Kaptain 0.73-2"
ENV LMSBUILD_DOCKER="${LMSBUILD_REPO}/${LMSBUILD_NAME}:${LMSBUILD_VERSION}" 
ENV LMSBUILD_PACKAGE="${LMSBUILD_PARENT}, debian-base-gui:9.6.0-gtk3"

# =========================================================================

RUN apt-get -y update \
 && apt-get -y upgrade \
 && apt-get -y install \
               bsdmainutils \
               groff-base \ 
               info \
               install-info \
               libpipeline1 \
               libqt4-qt3support \
               libqtcore4 \
               libqtgui4 \
               man \
 && apt-get clean all \
 && update-locale LANG=C.UTF-8 LC_MESSAGES=POSIX \
 && rm -rf /var/lib/apt/lists/* \ 
 && curl -fSL ${PKG_URL} \
         -o /usr/local/share/${PKG_NAME} \
 && dpkg -i /usr/local/share/${PKG_NAME} \
 && rm /usr/local/share/${PKG_NAME} \
 && printf "${LMSBUILD_DOCKER} (${LMSBUILD_PACKAGE}), %s @ %s\n" `date '+%Y-%m-%d'` `date '+%H:%M:%S'` >> /etc/ewsdocker-builds.txt 

# =========================================================================

COPY scripts/. / 

RUN chmod +x /usr/bin/lms/* \
 && chmod 775 /usr/local/bin/*

# =========================================================================

EXPOSE 9000

ENTRYPOINT ["/my_init", "--quiet"]
CMD ["/usr/bin/kaptain"]
