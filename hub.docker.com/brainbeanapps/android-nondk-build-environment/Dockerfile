FROM brainbeanapps/android-bare-build-environment:v1.2.0

LABEL maintainer="devops@brainbeanapps.com"

# Switch to root
USER root

# Install Android SDK components
RUN (yes | sdkmanager \
    "platforms;android-27" \
    "build-tools;29.0.2" \
    "build-tools;29.0.1" \
    "build-tools;29.0.0" \
    "build-tools;29.0.0-rc3" \
    "build-tools;29.0.0-rc2" \
    "build-tools;29.0.0-rc1" \
    "build-tools;28.0.3" \
    "build-tools;28.0.2" \
    "build-tools;28.0.1" \
    "build-tools;28.0.0" \
    "build-tools;28.0.0-rc2" \
    "build-tools;28.0.0-rc1" \
    "build-tools;27.0.3" \
    "build-tools;27.0.2" \
    "build-tools;27.0.1" \
    "build-tools;27.0.0" \
  )

# Switch to user
USER user
WORKDIR /home/user
