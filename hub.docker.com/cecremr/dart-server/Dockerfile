FROM ubuntu

ENV DART_VERSION=2.3.0
ENV DART_SDK=/usr/lib/dart
ENV PATH=/usr/lib/dart/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
ENV PUB_HOSTED_URL https://pub.flutter-io.cn
ENV FLUTTER_STORAGE_BASE_URL https://storage.flutter-io.cn

RUN apt-get -q update \
    && apt-get install --no-install-recommends -y -q gnupg2 wget git ca-certificates apt-transport-https openssh-client unzip \
    && wget --no-check-certificate -O /dartsdk.zip https://storage.googleapis.com/dart-archive/channels/stable/release/$DART_VERSION/sdk/dartsdk-linux-x64-release.zip \
    && unzip /dartsdk.zip \
    && mv /dart-sdk /usr/lib/dart \
    && rm /dartsdk.zip

CMD []