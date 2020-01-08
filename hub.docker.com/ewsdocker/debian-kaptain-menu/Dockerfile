# =========================================================================
# =========================================================================
#
#	Dockerfile
#	  Dockerfile for debian-kaptain-menu in a Docker container.
#
# =========================================================================
#
# @author Jay Wheeler.
# @version 9.6.2
# @copyright © 2017-2019. EarthWalk Software.
# @license Licensed under the GNU General Public License, GPL-3.0-or-later.
# @package ewsdocker/debian-kaptain-menu
# @subpackage Dockerfile
#
# =========================================================================
#
#	Copyright © 2017-2019. EarthWalk Software
#	Licensed under the GNU General Public License, GPL-3.0-or-later.
#
#   This file is part of ewsdocker/debian-kaptain-menu.
#
#   ewsdocker/debian-kaptain-menu is free software: you can redistribute 
#   it and/or modify it under the terms of the GNU General Public License 
#   as published by the Free Software Foundation, either version 3 of the 
#   License, or (at your option) any later version.
#
#   ewsdocker/debian-kaptain-menu is distributed in the hope that it will 
#   be useful, but WITHOUT ANY WARRANTY; without even the implied warranty 
#   of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
#   GNU General Public License for more details.
#
#   You should have received a copy of the GNU General Public License
#   along with ewsdocker/debian-kaptain-menu.  If not, see 
#   <http://www.gnu.org/licenses/>.
#
# =========================================================================
# =========================================================================
FROM ewsdocker/debian-kaptain:9.6.1

MAINTAINER Jay Wheeler <ewsdocker@gmail.com>

# =========================================================================

ENV DEBIAN_FRONTEND=noninteractive \
    LMSOPT_QUIET=0

# =========================================================================

ENV LMSBUILD_VERSION="9.6.2" 
ENV LMSBUILD_NAME=debian-kaptain-menu 
ENV LMSBUILD_REPO=ewsdocker 
ENV LMSBUILD_REGISTRY="" 

ENV LMSBUILD_PARENT="debian-kaptain:9.6.1"
ENV LMSBUILD_DOCKER="${LMSBUILD_REPO}/${LMSBUILD_NAME}:${LMSBUILD_VERSION}" 
ENV LMSBUILD_PACKAGE="${LMSBUILD_PARENT}"

# =========================================================================

RUN apt-get -y update \
 && apt-get -y upgrade \
 && apt-get clean all \
 && printf "${LMSBUILD_DOCKER} (${LMSBUILD_PACKAGE}), %s @ %s\n" `date '+%Y-%m-%d'` `date '+%H:%M:%S'` >> /etc/ewsdocker-builds.txt  
 
# =========================================================================

COPY scripts/. /

RUN ln -s /usr/bin/lms/kaptain-menu.sh /usr/bin/kaptain-menu \
 && chmod 775 /usr/bin/* \
 && chmod 775 /usr/local/bin/* \
 && chmod 600 /usr/local/share/applications/*.desktop \ 
 && chmod 600 /usr/local/share/lms/*.desktop  \
 && mkdir /kaptain


# =========================================================================
# =========================================================================
#
#    Volume		Purpose
#   ========    =======
#
#	/kaptain/lib        Directory containing the template library
#   /kaptain/source     Directory containing the command-template-name
#   /kaptain/command    Directory to place the generated executable
#   /kaptain/custom     Directory to place the customized grammar
#
#   /userbin
#
# =========================================================================
# =========================================================================

VOLUME /kaptain/lib 
VOLUME /kaptain/source 
VOLUME /kaptain/command 
VOLUME /kaptain/custom

VOLUME /userbin

# =========================================================================

ENTRYPOINT ["/my_init", "--quiet"]
CMD ["/bin/bash"]
