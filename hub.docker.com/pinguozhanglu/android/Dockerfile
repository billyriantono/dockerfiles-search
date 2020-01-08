FROM pinguoops/env:centos6
MAINTAINER zhanglu "zhanglu@camera360.com"

RUN yum -y install \
    glibc.i686 zlib.i686 libstdc++.i686 \
    java-1.7.0-openjdk.x86_64 \
    vixie-cron crontabs \
    && rm -rvf /var/cache/{yum,ldconfig}/* \
    && rm -rvf /etc/ld.so.cache \
    && yum clean all \
    && chkconfig --level 35 crond on

# -----------------------------------------------------------------------------
# Add user worker
# -----------------------------------------------------------------------------
RUN useradd -m -u 1000 worker \
    && echo "worker" | passwd --stdin worker \
    && echo 'worker  ALL=(ALL)  NOPASSWD: ALL' > /etc/sudoers.d/worker \
    && sed -i \
        -e 's/^#PermitRootLogin yes/PermitRootLogin no/g' \
        -e 's/^PermitRootLogin yes/PermitRootLogin no/g' \
        -e 's/^#PermitUserEnvironment no/PermitUserEnvironment yes/g' \
        -e 's/^PermitUserEnvironment no/PermitUserEnvironment yes/g' \
        /etc/ssh/sshd_config

ENV HOME /home/worker

# Main Android SDK
RUN cd ${HOME} \
    && wget -q http://dl.google.com/android/android-sdk_r24.2-linux.tgz \
    && tar xzf android-sdk_r24.2-linux.tgz \
    && rm -f android-sdk_r24.2-linux.tgz

# Other tools and resources of Android SDK
ENV ANDROID_HOME ${HOME}/android-sdk-linux
ENV PATH ${PATH}:${ANDROID_HOME}/tools:${ANDROID_HOME}/platform-tools
RUN ( sleep 5 && while [ 1 ]; do sleep 1; echo y; done ) | android update sdk --all --filter tools,platform-tools,build-tools-22.0.1,android-22,sys-img-armeabi-v7a-android-22,addon-google_apis-google-22,extra-android-support --no-ui --force

RUN mkdir -p /var/run/sshd
RUN chown -R worker.worker ${HOME} \
    && chmod 750 ${HOME}


EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]
