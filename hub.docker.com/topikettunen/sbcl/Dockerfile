FROM ubuntu:bionic
LABEL maintainer="Topi Kettunen <topi@kettunen.io>"

RUN set -ex; \
	apt-get update; \
	apt-get install -y --no-install-recommends \
		# sbcl required for compiling
		sbcl \
		curl \
		git \
		make \
		build-essential \
		libz-dev \
	; \
	rm -rf /var/lib/apt/lists/*

# To build small container with CL we need to build SBCL with flag '--with-sb-linkable-runtime' and '--with-sb-dynamic-core'
RUN set -ex && \
	git clone git://git.code.sf.net/p/sbcl/sbcl && \
	cd sbcl && \
	sh make.sh \
		--fancy \
		--with-sb-linkable-runtime \
		--with-sb-dynamic-core && \
	sh install.sh

RUN set -ex && \
	curl -o /tmp/ql.lisp http://beta.quicklisp.org/quicklisp.lisp && \
	sbcl --no-sysinit --no-userinit --load /tmp/ql.lisp \
		--eval '(quicklisp-quickstart:install :path "common-lisp")' \
		--quit && \
	echo '#-quicklisp\n\
  (let ((quicklisp-init #P"/common-lisp/setup.lisp"))\n\
    (when (probe-file quicklisp-init)\n\
	(load quicklisp-init)))\n' > /root/.sbclrc
