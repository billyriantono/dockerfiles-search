FROM hlhr202/flutter-android-base:28

ENV FLUTTER_CHANNEL="stable"
ENV FLUTTER_VERSION="v1.9.1+hotfix.6"
ENV FLUTTER_HOME="/opt/flutter"

ENV PATH="${FLUTTER_HOME}/bin:${FLUTTER_HOME}/bin/cache/dart-sdk/bin:$PATH"

RUN curl https://storage.googleapis.com/flutter_infra/releases/stable/linux/flutter_linux_${FLUTTER_VERSION}-${FLUTTER_CHANNEL}.tar.xz -o /opt/flutter.tar.xz \
    && tar xf /opt/flutter.tar.xz -C /opt \
    && rm /opt/flutter.tar.xz \
    && flutter config  --no-analytics \
    && flutter precache
    
RUN flutter doctor -v