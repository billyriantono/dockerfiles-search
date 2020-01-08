FROM alpine:3.8

ARG QT_VERSION=5.10.1-r0

RUN apk update && \
    apk add --no-cache \
		g++ \
		make \
		qt5-qtbase-dev=${QT_VERSION} \
		qt5-qtquickcontrols2-dev=${QT_VERSION} && \
	ln /usr/bin/qmake-qt5 /usr/bin/qmake

