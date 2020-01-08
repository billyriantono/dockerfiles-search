FROM ubuntu:12.04

MAINTAINER zhanglu "zhanglu@camera360.com"

RUN apt-get update -qq

# Dependencies to execute android
RUN apt-get install -y --no-install-recommends openjdk-7-jdk libgd2-xpm ia32-libs ia32-libs-multiarch \
        bzip2 unzip file vim curl telnet wget git \
        openssl openssh-server sudo python-pip \
    && apt-get clean
        
RUN pip install supervisor \
    && rm -rvf /tmp/*

RUN ln -sf /usr/share/zoneinfo/Asia/Chongqing /etc/localtime \
    && sed -i \
      -e 's/^UsePAM yes/#UsePAM yes/g' \
      -e 's/^#UsePAM no/UsePAM no/g' \
      -e 's/#UsePrivilegeSeparation.*/UsePrivilegeSeparation no/g' \
      -e 's/^#UseDNS yes/UseDNS no/g' \
      /etc/ssh/sshd_config \
    && echo 'root:root' | chpasswd \
    && rm -rf /etc/ssh/ssh_host_rsa_key \
    && ssh-keygen -q -b 1024 -N '' -t rsa -f /etc/ssh/ssh_host_rsa_key \
    && rm -rf /etc/ssh/ssh_host_dsa_key \
    && ssh-keygen -q -b 1024 -N '' -t dsa -f /etc/ssh/ssh_host_dsa_key
#    && echo "NETWORKING=yes" > /etc/sysconfig/network

# -----------------------------------------------------------------------------
# Add user worker
# -----------------------------------------------------------------------------
RUN useradd -m -u 1000 -s /bin/bash worker \
    && echo 'worker:worker' | chpasswd \
    && echo 'worker  ALL=(ALL)  NOPASSWD: ALL' > /etc/sudoers.d/worker \
    && sed -i \
        -e 's/^#PermitRootLogin yes/PermitRootLogin no/g' \
        -e 's/^PermitRootLogin yes/PermitRootLogin no/g' \
        /etc/ssh/sshd_config

ENV HOME /home/worker

# Main Android SDK
RUN cd ${HOME} && wget -q http://dl.google.com/android/android-sdk_r24.2-linux.tgz
RUN cd ${HOME} && tar xzf android-sdk_r24.2-linux.tgz
RUN cd ${HOME} && rm -f android-sdk_r24.2-linux.tgz

# Other tools and resources of Android SDK
ENV ANDROID_HOME ${HOME}/android-sdk-linux
ENV PATH ${PATH}:${ANDROID_HOME}/tools:${ANDROID_HOME}/platform-tools
RUN ( sleep 5 && while [ 1 ]; do sleep 1; echo y; done ) | android update sdk --all --filter tools,platform-tools,build-tools-22.0.1,android-22,sys-img-armeabi-v7a-android-22,addon-google_apis-google-22,extra-android-support --no-ui --force
# RUN ( sleep 5 && while [ 1 ]; do sleep 1; echo y; done ) | android update sdk --filter platform-tools,build-tools-19.0.3,android-17,extra-android-support --no-ui --force
# RUN ( sleep 5 && while [ 1 ]; do sleep 1; echo y; done ) | android update sdk -a --no-ui --force

RUN mkdir -p /var/run/sshd
RUN chown -R worker.worker /home/worker/

EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]
