FROM golang:1.9.3
RUN apt-get -y update && apt-get install -y vim unzip
WORKDIR /opt
RUN wget https://dl.google.com/android/repository/android-ndk-r15c-linux-x86_64.zip \
&& unzip android-ndk-r15c-linux-x86_64.zip
RUN ls -l && /opt/android-ndk-r15c/build/tools/make_standalone_toolchain.py \
		--api=14 --install-dir=/toolchain \
		--arch=arm --stl libc++
ENV CC="/toolchain/bin/arm-linux-androideabi-gcc"
ENV	CXX="/toolchain/bin/arm-linux-androideabi-g++"
ENV	CGO_CFLAGS="-march=armv7-a"
ENV	GOOS=android
ENV	GOARCH=arm
ENV	GOARM=7
ENV	CGO_ENABLED=1
CMD [ "bash" ]

