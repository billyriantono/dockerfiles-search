FROM openjdk:8
MAINTAINER Ivan Zinovyev <izinovyev42@gmail.com>

ENV VERSION_SDK_TOOLS "4333796"
ENV BUNDLETOOL_VERSION 0.12.0

ENV ANDROID_HOME "/sdk"
ENV PATH "$PATH:${ANDROID_HOME}/tools;"

RUN apt-get -qq update  && \
    apt-get install -qqy --no-install-recommends \ 
    locales \
    ant \
    ca-certificates-java \
    bzip2 \
    curl \
    git-core \
    html2text \
    libc6-i386 \
    lib32stdc++6 \
    lib32gcc1 \
    lib32ncurses5 \
    lib32z1 \
    tar \
    unzip \
    build-essential \
    vim-common \
    locales
    
ENV LANG en_US.utf8

RUN  rm -rf /var/lib/apt/lists/* && localedef -i en_US -c -f UTF-8 -A /usr/share/locale/locale.alias en_US.UTF-8 
RUN  update-ca-certificates -f

RUN curl -s https://dl.google.com/android/repository/sdk-tools-linux-${VERSION_SDK_TOOLS}.zip > /sdk.zip && \
    unzip /sdk.zip -d /sdk && \
    rm -v /sdk.zip
    
RUN mkdir -p $ANDROID_HOME/licenses/ \
  && echo "8933bad161af4178b1185d1a37fbf41ea5269c55\nd56f5187479451eabf01fb78af6dfcb131a6481e\n24333f8a63b6825ea9c5514f83c2829b004d1fee" > $ANDROID_HOME/licenses/android-sdk-license \
  && echo "84831b9409646a918e30573bab4c9c91346d8abd\n504667f4c0de7af1a06de9f4b1727b84351f2910" > $ANDROID_HOME/licenses/android-sdk-preview-license

ADD packages.txt /sdk
RUN mkdir -p /root/.android && \
  touch /root/.android/repositories.cfg && \
  ${ANDROID_HOME}/tools/bin/sdkmanager --update 

RUN while read -r package; do PACKAGES="${PACKAGES}${package} "; done < /sdk/packages.txt && \
    ${ANDROID_HOME}/tools/bin/sdkmanager ${PACKAGES}
    
# Install bundletool
ADD https://github.com/google/bundletool/releases/download/${BUNDLETOOL_VERSION}/bundletool-all-${BUNDLETOOL_VERSION}.jar /usr/bin/bundletool.jar
RUN echo -e "#!/bin/sh\nDIR=\$(dirname \$0)\njava -jar \$DIR/bundletool.jar \$@" > /usr/bin/bundletool && \
    chmod +x /usr/bin/bundletool    

RUN yes | ${ANDROID_HOME}/tools/bin/sdkmanager --licenses
