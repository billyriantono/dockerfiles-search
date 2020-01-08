#PhantomJS

FROM ubuntu:14.04
MAINTAINER Renan Gomes

ENV PHANTOMJS_VERSION master

#prereqs
RUN apt-get -yqq update && \
    apt-get install -yq git nano  build-essential g++ flex bison gperf ruby perl python libsqlite3-dev libfontconfig1-dev libicu-dev libfreetype6 libssl-dev libpng-dev libjpeg-dev build-essential g++ flex bison gperf ruby perl libsqlite3-dev libfontconfig1-dev libicu-dev libfreetype6 libssl-dev libpng-dev libjpeg-dev python libx11-dev libxext-dev ttf-mscorefonts-installer && apt-get clean

#build
RUN cd /tmp && \
    git clone git://github.com/RenanGBarreto/phantomjs.git && \
    cd phantomjs/ && \
    git checkout $PHANTOMJS_VERSION && git submodule init && git submodule update
	
RUN cd /tmp/phantomjs/ && \
    sed -i -e 's/, m_allowStar(false)/, m_allowStar(true)/g' /tmp/phantomjs/src/qt/qtwebkit/Source/WebCore/page/ContentSecurityPolicy.cpp  && \
    sed -i -e 's/, m_allowEval(false)/, m_allowEval(true)/g' /tmp/phantomjs/src/qt/qtwebkit/Source/WebCore/page/ContentSecurityPolicy.cpp  && \
    sed -i -e 's/, m_allowInline(false)/, m_allowInline(true)/g' /tmp/phantomjs/src/qt/qtwebkit/Source/WebCore/page/ContentSecurityPolicy.cpp

RUN cd /tmp/phantomjs/ && \
    echo y | python ./build.py && \
    cp bin/phantomjs /usr/bin/

ENTRYPOINT [ "/bin/bash" ]
