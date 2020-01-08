# ====================================================================== #
# Android SDK Docker Image
# ====================================================================== #

# Base image
# ---------------------------------------------------------------------- #
FROM kaminomobile/android-sdk:110

# Author
# ---------------------------------------------------------------------- #
LABEL blazsolar "blaz@kamino.si"

ARG PLATFORM_VERSION=29
ARG NDK_VERSION=20.0.5594570
ARG BUILD_TOOLS=29.0.2

# install build tools and platform
RUN sdkmanager "platform-tools" "build-tools;${BUILD_TOOLS}" "platforms;android-${PLATFORM_VERSION}" "cmake;3.10.2.4988404" "ndk;${NDK_VERSION}"

ENV ANDROID_NDK ${ANDROID_HOME}/ndk/${NDK_VERSION}