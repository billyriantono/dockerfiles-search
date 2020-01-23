ARG TAG=latest

FROM cnarf/buster:${TAG}

LABEL maintainer="cnarf@charline"
LABEL description="The graal?"

RUN apt-get install --no-install-recommends -y \
    make \
    g++-8 libstdc++6-8-dbg gcc-8-locales libgomp1-dbg libitm1-dbg libatomic1-dbg libasan5-dbg liblsan0-dbg libtsan0-dbg libubsan1-dbg libmpx2-dbg libquadmath0-dbg \
    lcov \
    curl ca-certificates \
&& apt-get clean \
&& /root/finalize.sh;
