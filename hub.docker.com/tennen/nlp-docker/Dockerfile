#   Copyright [2018] [Kurohashi-Kawahara lab, Kyoto University]
#
#   Licensed under the Apache License, Version 2.0 (the "License");
#   you may not use this file except in compliance with the License.
#   You may obtain a copy of the License at
#
#       http://www.apache.org/licenses/LICENSE-2.0
#
#   Unless required by applicable law or agreed to in writing, software
#   distributed under the License is distributed on an "AS IS" BASIS,
#   WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
#   See the License for the specific language governing permissions and
#   limitations under the License.

FROM alpine:3.8

ARG JUMANPP_VERSION=1.01

ARG TARGET=jumanpp
ARG EXTENTION=tar.xz
ARG URL=http://lotus.kuee.kyoto-u.ac.jp/nl-resource/${TARGET}/${TARGET}-${JUMANPP_VERSION}.${EXTENTION}
ARG INST_PATH=/usr/local/src/${TARGET}-${JUMANPP_VERSION}.${EXTENTION}
ARG REMOVE_PATH=${TARGET}-${JUMANPP_VERSION}/src

WORKDIR /usr/local/src/

# prepare
# after delete
RUN apk update && \
	apk --no-cache --virtual=${TARGET}_rm add \
	curl \
	xz \
	which \
	bzip2 \
	gcc \
	g++ \
	make \
	;\
# remains
    apk --no-cache --virtual=${TRAGET} add \
        libstdc++ \
        libgcc \
        boost-dev \
        bash \
	; \
# JUMANPP
    curl -o ${INST_PATH} "${URL}" ;\
    tar Jxvf ${TARGET}-${JUMANPP_VERSION}.${EXTENTION} ;\
    cd ${TARGET}-${JUMANPP_VERSION} ;\
    ./configure ; make ; make install ;\
    cd ../ ; rm -rf ${REMOVE_PATH} ;\
    rm -rf ${TARGET}-${JUMANPP_VERSION}.${EXTENTION} ;\
    apk del ${TARGET}_rm

CMD ["jumanpp"]

