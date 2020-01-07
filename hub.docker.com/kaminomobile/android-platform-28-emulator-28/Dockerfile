# ====================================================================== #
# Android Emulator Docker Image
# ====================================================================== #

ARG PLATFOM_VERSION=28

# Base image
# ---------------------------------------------------------------------- #
FROM kaminomobile/android-platform-${PLATFOM_VERSION}:112

# Author
# ---------------------------------------------------------------------- #
LABEL blazsolar "blaz@kamino.si"

ARG EMULATOR_SDK_LEVEL=28

USER root

# deps 
RUN apt-get update -y && \
	apt-get install qemu-kvm -y

RUN usermod -aG kvm jenkins

USER jenkins

# install build tools and platform
RUN sdkmanager "emulator" "tools" "system-images;android-${EMULATOR_SDK_LEVEL};google_apis;x86"

# Emulator
# RUN echo "no" | avdmanager create avd -n emulator_avd -k "system-images;android-${EMULATOR_SDK_LEVEL};google_apis;x86" -c 4096M
RUN echo "no" | avdmanager create avd -n emulator_avd -k "system-images;android-${EMULATOR_SDK_LEVEL};google_apis;x86"

# Cache image
RUN dd if=/dev/zero of=$HOME/.android/avd/emulator_avd.avd/cache.img bs=10M count=1 \
    && mkfs.ext4 -F $HOME/.android/avd/emulator_avd.avd/cache.img

COPY --chown=jenkins:jenkins start_emulator_debug.sh /usr/local/bin/start-emulator

RUN adb start-server \
    adv kill-server