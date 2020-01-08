FROM thyrlian/android-sdk
RUN apt-get update
RUN apt-get install -y xz-utils
RUN wget -q https://storage.googleapis.com/flutter_infra/releases/stable/linux/flutter_linux_v1.0.0-stable.tar.xz
RUN tar -xf flutter_linux_*.tar.xz
ENV PATH="`${PATH}:/flutter/bin"
RUN sdkmanager "platform-tools" "platforms;android-28" "build-tools;28.0.3"
RUN yes | sdkmanager --licenses
