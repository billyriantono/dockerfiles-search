FROM moosivp/moos-ivp:r8904
LABEL maintainer = Conlan Cesar <conlanc@csail.mit.edu>

ENV MOOS="moos-ivp-cc"

ENV PATH="/home/moos/${MOOS}/bin:${PATH}"
ENV IVP_BEHAVIOR_DIRS="${IVP_BEHAVIOR_DIRS}:/home/moos/${MOOS}/lib"

USER root
RUN apt-get -y update && DEBIAN_FRONTEND=noninteractive apt-get install -y libssl-dev \
    libboost-system-dev libboost-thread-dev libboost-coroutine-dev libboost-context-dev \
    libsndfile-dev libopus-dev portaudio19-dev \
    libprotobuf-dev protobuf-compiler liblog4cpp5-dev && apt-get -y clean
USER moos

COPY --chown=moos:moos "." "/home/moos/${MOOS}"

RUN cd "${HOME}/${MOOS}" && ./build.sh

