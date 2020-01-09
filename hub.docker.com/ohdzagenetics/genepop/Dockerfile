# Header
FROM ubuntu:latest

ENV LATEST_VERSION="4" \
    EXE_NAME="Genepop"

# Install dependencies
RUN apt-get update && apt-get -y install \
	g++ \
    unzip

# Download and unpack software
RUN mkdir "${EXE_NAME}"
ADD http://kimura.univ-montp2.fr/%7Erousset/GenepopV${LATEST_VERSION}.zip ${EXE_NAME}/${EXE_NAME}.tar.gz
RUN cd ${EXE_NAME} && \
    unzip ${EXE_NAME}.tar.gz && \
    unzip sources.zip && \
    g++ -DNO_MODULES -o ${EXE_NAME} GenepopS.cpp -O3 && \
    cp ${EXE_NAME} /usr/local/bin/
