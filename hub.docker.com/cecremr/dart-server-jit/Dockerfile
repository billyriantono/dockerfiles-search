FROM google/dart
ADD run.sh /dart_runtime/
RUN chmod 755 /dart_runtime/run.sh && chown root:root /dart_runtime/run.sh
ENV PUB_HOSTED_URL https://pub.flutter-io.cn
ENV FLUTTER_STORAGE_BASE_URL https://storage.flutter-io.cn