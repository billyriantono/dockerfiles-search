FROM celforyon/nodejs:10

LABEL maintainer="Alexis Pereda <alexis@pereda.fr>"
LABEL version="0.3"
LABEL description="Base for a Godbolt Compiler Explorer container"

RUN DEBIAN_FRONTEND=noninteractive apt update \
	&& apt install --no-install-recommends --no-install-suggests -y \
		binutils git gcc libc6-dev nasm make yarn \
	&& git clone https://github.com/mattgodbolt/compiler-explorer.git /compiler-explorer \
	&& cd /compiler-explorer \
	&& sed -i '/node_modules\/bower\/bin\/bower install/c\\t\/usr\/bin\/nodejs .\/node_modules\/bower\/bin\/bower install --allow-root' /compiler-explorer/Makefile \
	&& sed -i 's|--exec $(NODE) $(NODE_ARGS) -- ./app.js $(EXTRA_ARGS)||' /compiler-explorer/Makefile \
	&& apt autoremove --purge -y \
	&& apt autoclean -y \
	&& rm -rf /var/cache/apt/* /var/lib/apt/lists/* /tmp/* \
	&& useradd -md /home/user user \
	&& chown -R user:user /compiler-explorer

WORKDIR /compiler-explorer

USER user
RUN make
USER root
