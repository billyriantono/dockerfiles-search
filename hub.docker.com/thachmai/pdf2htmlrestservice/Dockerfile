FROM thachmai/pdf2htmlex
MAINTAINER contact@thachmai.info

# Install mono 3.10
RUN apt-get update \
	&& apt-get install -y curl unzip \
	autoconf \
	automake \
	build-essential \
	libtool

RUN apt-key adv --keyserver pgp.mit.edu --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF
RUN echo "deb http://download.mono-project.com/repo/debian wheezy/snapshots/3.10.0 main" > /etc/apt/sources.list.d/mono-xamarin.list \
	&& apt-get update \
	&& apt-get install -y mono-devel fsharp mono-vbnc nuget 
RUN mozroots --machine --import --sync --quiet

# Install ASP.NET
ENV KRE_VERSION 1.0.0-beta1
ENV KRE_USER_HOME /opt/kre

RUN curl -sSL https://raw.githubusercontent.com/aspnet/Home/v$KRE_VERSION/kvminstall.sh | sh
RUN bash -c "source $KRE_USER_HOME/kvm/kvm.sh \
	&& kvm install $KRE_VERSION -a default \
	&& kvm alias default | xargs -i ln -s $KRE_USER_HOME/packages/{} $KRE_USER_HOME/packages/default"

RUN LIBUV_VERSION=1.0.0-rc2 \
	&& curl -sSL https://github.com/joyent/libuv/archive/v${LIBUV_VERSION}.tar.gz | tar zxfv - -C /usr/local/src \
	&& cd /usr/local/src/libuv-$LIBUV_VERSION \
	&& sh autogen.sh && ./configure && make && make install \
	&& rm -rf /usr/local/src/libuv-$LIBUV_VERSION \
	&& ldconfig
ENV PATH $PATH:$KRE_USER_HOME/packages/default/bin

RUN rm -rf /var/lib/apt/lists/*

EXPOSE 5004
