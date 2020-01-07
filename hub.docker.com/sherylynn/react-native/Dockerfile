# Pull base image.
FROM sherylynn/android-ndk
MAINTAINER Sherylynn <352281674@qq.com>

# ——————————
# Install Basic React-Native packages
# ——————————
RUN npm install \
        react-native-cli \
        rnpm \
        react-native-update-cli -g && \
    npm cache clean