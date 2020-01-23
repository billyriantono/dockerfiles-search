# ========================================================================================
# ========================================================================================
#
#    Dockerfile
#      Dockerfile for lms-utilities container to generate lms-library.
#
# ========================================================================================
#
# @author Jay Wheeler.
# @version 0.1.2
# @copyright © 2018, 2019. EarthWalk Software.
# @license Licensed under the GNU General Public License, GPL-3.0-or-later.
# @package lms-utilities
# @subpackage Dockerfile
#
# ========================================================================================
#
#	Copyright © 2018, 2019. EarthWalk Software
#	Licensed under the GNU General Public License, GPL-3.0-or-later.
#
#   This file is part of ewsdocker/lms-utilities.
#
#   ewsdocker/lms-utilities is free software: you can redistribute 
#   it and/or modify it under the terms of the GNU General Public License 
#   as published by the Free Software Foundation, either version 3 of the 
#   License, or (at your option) any later version.
#
#   ewsdocker/lms-utilities is distributed in the hope that it will 
#   be useful, but WITHOUT ANY WARRANTY; without even the implied warranty 
#   of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
#   GNU General Public License for more details.
#
#   You should have received a copy of the GNU General Public License
#   along with ewsdocker/lms-utilities.  If not, see 
#   <http://www.gnu.org/licenses/>.
#
# ========================================================================================
# ========================================================================================

# ========================================================================================
#
#	             Build-time arguements (--build-arg)
#
# ========================================================================================
#
#   ARG_NAME = name of the tarball (w/o version) to create
#   ARG_DIR  = name of the target directory (defaults to "usr")
#   ARG_DEST = path to the archive storage directory
#
# ========================================================================================
#
#   ARGBUILD_REPO = repository name of the image being built
#   ARGBUILD_REGISTRY = registry name of the image being built
#
#   ARGBUILD_NAME = version of the image being built
#   ARGBUILD_VERSION = name of the image being built
#
# ========================================================================================
#
#   ARG_FROM_REPO = repository name of the build-from image
#   ARG_FROM_VERS = version of the build-from image
#   ARG_FROM_PARENT = name of the build-from image parent
#
# ========================================================================================

ARG ARG_NAME="lms-library"
ARG ARG_DIR="usr"
ARG ARG_DEST="/repo"

ARG ARGBUILD_REGISTRY=""
ARG ARGBUILD_REPO=ewsdocker

ARG ARGBUILD_NAME="lms-utilities" 
ARG ARGBUILD_VERSION="0.1.2"

# ========================================================================================
# ========================================================================================

ARG ARG_FROM_PARENT="alpine-base"
ARG ARG_FROM_REPO="ewsdocker/${ARG_FROM_PARENT}"
ARG ARG_FROM_VERS="3.8.1"

FROM ${ARG_FROM_REPO}:${ARG_FROM_VERS}

# ========================================================================================
# ========================================================================================

# ========================================================================================
#
#   Re-declare build-args, but don't change any assignments 
#       (makes the settings available inside the build)
#
# ========================================================================================

ARG ARG_NAME
ARG ARG_DIR
ARG ARG_DEST

ARG ARGBUILD_VERSION

ARG ARGBUILD_NAME 
ARG ARGBUILD_REPO
ARG ARGBUILD_REGISTRY

ARG ARG_FROM_REPO
ARG ARG_FROM_VERS
ARG ARG_FROM_PARENT

# ========================================================================================
#
#	Assign to environment variables to persist
#
#   LMSUTIL_NAME = name of the tarball (w/o version) to create
#   LMSUTIL_DIR  = name of the target directory (defaults to "usr")
#   LMSUTIL_DEST = path to the archive storage directory
#
# ========================================================================================

ENV LMSUTIL_NAME=${ARG_NAME} \
    LMSUTIL_DIR=${ARG_DIR} \
    LMSUTIL_DEST=${ARG_DEST} \
    \
    \
    LMS_BASE="/usr/local" \
    \
    \
    LMSBUILD_REGISTRY=${ARGBUILD_REGISTRY} \
    LMSBUILD_REPO=${ARGBUILD_REPO} \
    \
	\
    LMSBUILD_NAME=${ARGBUILD_NAME} \
    LMSBUILD_VERSION=${ARGBUILD_VERSION} \
    \
    \
    LMSBUILD_DOCKER="${LMSBUILD_REPO}/${LMSBUILD_NAME}:${LMSBUILD_VERSION}" \
    LMSBUILD_PACKAGE="${ARG_FROM_REPO}:${ARG_FROM_VERS}" \
    LMSBUILD_BASE="${ARG_FROM_PARENT}:${ARG_FROM_VERS}"

# ========================================================================================

COPY scripts/. "/${LMSUTIL_NAME}"

# ========================================================================================

RUN \
#
#   build apk cache, upgrade to latest packages, and create debian-base
#
    apk update \
 && apk upgrade \
 && apk add bash \
            bash-doc \
            bash-completion \
            binutils \
            coreutils \
            curl \
            dbus \
            findutils \
            grep \
            nano \
            pciutils \
            shadow \
            unzip \
            util-linux \
            wget \
            zip \
 && rm -rf /var/cache/apk/* \
#
#  setup lms-utilities installer
#
 && chmod -R +x /${LMSUTIL_NAME}/usr/bin/lms/lms-utilities.sh \
 && ln -s /${LMSUTIL_NAME}/usr/bin/lms/lms-utilities.sh /usr/bin/lms-utilities 

# ========================================================================================

CMD ["lms-utilities"]
