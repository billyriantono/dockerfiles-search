FROM fedora:30

ENV JAVA_HOME=/usr/lib/jvm/java \
	ANDROID_SDK_ROOT=/opt/android-sdk \
	PATH="${ANDROID_SDK_ROOT}/tools:${ANDROID_SDK_ROOT}/platform-tools:${PATH}"

RUN dnf module enable -y nodejs:12/default && \
	dnf upgrade --setopt=install_weak_deps=False --best -y && \
	dnf module install -y nodejs:12/default && \
	dnf install --setopt=install_weak_deps=False --best -y \
		make unzip curl \
		java-1.8.0-openjdk-devel \
		wine-core.i686 \
		gradle && \
	mkdir -p $ANDROID_SDK_ROOT && cd $ANDROID_SDK_ROOT && \
	curl -o sdk-tools.zip https://dl.google.com/android/repository/sdk-tools-linux-4333796.zip && \
	unzip sdk-tools.zip && \
	rm sdk-tools.zip && \
	yes | $ANDROID_SDK_ROOT/tools/bin/sdkmanager --licenses && \
	yes | $ANDROID_SDK_ROOT/tools/bin/sdkmanager "platform-tools" "platforms;android-28" "build-tools;28.0.3" && \
	dnf clean all -y
