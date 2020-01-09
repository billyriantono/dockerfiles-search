FROM quay.io/bitriseio/android:latest

WORKDIR /etc/flutter
RUN wget https://storage.googleapis.com/flutter_infra/releases/stable/linux/flutter_linux_v1.9.1+hotfix.4-stable.tar.xz && \
    tar xf flutter_linux_v1.9.1+hotfix.4-stable.tar.xz

ENV PATH="/etc/flutter/flutter/bin:${PATH}"
RUN flutter doctor

WORKDIR /bitrise/src