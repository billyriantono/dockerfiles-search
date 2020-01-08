# Android development environment for ubuntu.
# Adapted from tracer0tong's android emulator version 0.0.5

FROM strongandstable/docker-android

# Specially for SSH access and port redirection
ENV ROOTPASSWORD android

# Expose ADB, ADB control and VNC ports
EXPOSE 22
# Daemon port
EXPOSE 5037
EXPOSE 5554
# adb connect <ip>:<port>
EXPOSE 5555
EXPOSE 5900

# Disable interactive configuration
ENV DEBIAN_FRONTEND noninteractive
RUN echo "debconf shared/accepted-oracle-license-v1-1 select true" | debconf-set-selections && \
    echo "debconf shared/accepted-oracle-license-v1-1 seen true" | debconf-set-selections

# Update packages
RUN apt-get -y update && \
    apt-get -y install software-properties-common bzip2 ssh net-tools openssh-server socat curl

# Graphics blirary
RUN apt-get -y install libgl1-mesa-dev && \
    # KVM
    apt-get -y install qemu-kvm libvirt-bin ubuntu-vm-builder bridge-utils

# Remove apt-get update package lists
RUN rm -rf /var/lib/apt/lists/*

# Update env path
ENV PATH $PATH:$ANDROID_HOME/tools
ENV PATH $PATH:$ANDROID_HOME/platform-tools
ENV JAVA_HOME /usr/lib/jvm/java-8-openjdk-amd64

# QT library denendency
ENV LD_LIBRARY_PATH $LD_LIBRARY_PATH:$ANDROID_HOME/tools/lib64/qt/lib

# Install latest android tools and android-23 x86)64 system image
RUN echo y | $ANDROID_HOME/tools/bin/sdkmanager --verbose "system-images;android-25;google_apis;x86_64" emulator

# Create fake keymap file
RUN mkdir $ANDROID_HOME/tools/keymaps && \
    touch $ANDROID_HOME/tools/keymaps/en-us

# Run sshd
RUN mkdir /var/run/sshd && \
    echo "root:$ROOTPASSWORD" | chpasswd && \
    sed -i 's/PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config && \
    sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd && \
    echo "export VISIBLE=now" >> /etc/profile

ENV NOTVISIBLE "in users profile"

# Add entrypoint
ADD entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]