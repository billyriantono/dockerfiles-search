FROM containership/android-base:latest

RUN npm install -g react-native-cli

RUN mkdir -p /app
RUN mkdir -p ~/.ssh

# Google Play services, revision 39
RUN echo "y" | android update sdk -u -a -t $(android list sdk -a | grep "Google Play services, revision 39" | awk '{ print $1 }' | sed 's/.$//')

# Google Repository, revision 46
RUN echo "y" | android update sdk -u -a -t $(android list sdk -a | grep "Google Repository, revision 46" | awk '{ print $1 }' | sed 's/.$//')

# Android SDK Build-tools, revision 25.0.2
RUN echo "y" | android update sdk -u -a -t $(android list sdk -a | grep "Android SDK Build-tools, revision 25.0.2" | awk '{ print $1 }' | sed 's/.$//')

# 35- SDK Platform Android 7.1.1, API 25
RUN echo "y" | android update sdk -u -a -t $(android list sdk -a | grep "35- SDK Platform Android 7.1.1, API 25" | awk '{ print $1 }' | sed 's/.$//')

WORKDIR /app
