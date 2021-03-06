FROM friism/mono:alpha

ENV DNX_VERSION latest
ENV DNX_PATH /root/.dnx

RUN apt-get -qq update && apt-get -qqy install unzip

RUN touch ~/.profile
RUN curl -sSL https://raw.githubusercontent.com/aspnet/Home/dev/dnvminstall.sh | DNX_BRANCH=v$DNX_VERSION sh
RUN bash -c "source $DNX_PATH/dnvm/dnvm.sh \
	&& dnvm install -u $DNX_VERSION -a default \
	&& dnvm alias default | xargs -i ln -s $DNX_PATH/runtimes/{} $DNX_PATH/runtimes/default"

# Install libuv for Kestrel from source code (binary is not in wheezy and one in jessie is still too old)
RUN apt-get -qqy install \
	autoconf \
	automake \
	build-essential \
	libtool
RUN LIBUV_VERSION=1.4.2 \
	&& curl -sSL https://github.com/libuv/libuv/archive/v${LIBUV_VERSION}.tar.gz | tar zxfv - -C /usr/local/src \
	&& cd /usr/local/src/libuv-$LIBUV_VERSION \
	&& sh autogen.sh && ./configure && make && make install \
	&& rm -rf /usr/local/src/libuv-$LIBUV_VERSION \
	&& ldconfig

ENV PATH $PATH:$DNX_PATH/runtimes/default/bin
