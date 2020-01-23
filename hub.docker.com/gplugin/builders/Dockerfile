FROM opensuse:tumbleweed

MAINTAINER Gary Kramlich <grim@reaperworld.com>

RUN set -ex && \
	zypper --gpg-auto-import-keys refresh && \
	zypper -n install \
		ca-certificates-mozilla \
		meson ninja gcc mercurial \
		rpm-build \
		help2man libxslt-tools gettext-tools \
		glib2-devel gobject-introspection-devel \
		gtk3-devel gtk-doc libgladeui-2-devel \
		python3-devel python3-gobject python-gobject-devel \
		lua-devel lua-lgi \
	&& \
	zypper -n clean

CMD ["/build.sh"]

ENV DISTRIBUTION=opensuse \
    VERSION=tumbleweed \
    ARCH=amd64

COPY rpm/build.sh /build.sh
