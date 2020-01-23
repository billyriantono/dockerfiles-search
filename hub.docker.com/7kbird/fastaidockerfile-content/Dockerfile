
# Dockerfile: 0x666f6f/alpine-python3-minimal:optimised-3.7
# Alpine Linux 3.9.3 + Python 3.7.3 + Pip 19.1
###########################################
# This image uses the Alpine Linux 3.9.3 base, and uses a multistage framework to compile from source a diskspace-optimised Python3 (3.7.3).
# This image is intended to produce the smallest possible Python3 base image with the latest stable Python and Alpine Linux releases.

###########################################
# STAGE ONE (builder)

FROM alpine:3.9 as builder
MAINTAINER Nicholas Laurent 0x666f6f@nym.hush.com
ARG PYTHON_VERSION="3.7.3" 
ENV \
  LANG="C.UTF-8" \
  PYTHONHOME="/usr/local" \
  PYTHONPATH="/usr/local/bin" \
  LD_LIBRARY_PATH="${LD_LIBRARY_PATH}:${PYTHONHOME}/lib" \
  C_INCLUDE_PATH="${C_INCLUDE_PATH}:${PYTHONHOME}/include" \
  PATH="${PYTHONPATH}:${PATH}"
RUN set -e \
  # Install fetch/unpack dependencies (Optionally, add GPG libraries here for sig validation of the downloaded file.)
  && echo -n "Installing fetcher dependencies... " \
    && apk --no-cache add --virtual .fetch-deps wget xz-dev >/dev/null 2>&1 \
    && echo "Done." \
  \
  # Install Python dependencies.
  #
  # - bzip2, xz-dev, zlib-dev: (de)Compression libraries.
  # - expat-dev: Expat XML parser, including as a dependency for cElementTree. Python linking requirement (./configure option).
  # - gdbm-dev: GNU dbm is a set of database routines that use extensible hashing.
  # - libffi-dev: High-level programming interface. Python linking requirement necessary for the compilation of the _ctypes module.
  # - ncurses-dev: New Curses terminal-based API library.
  # - openssl-dev: SSL library.
  # - sqlite-dev: SQLite3 (./configure option).
  # - [removed] tk-dev + tcl-dev: Tkinter libraries. Intentionally not installed and thus not compiled as Python module and libraries.
  \  
  && echo -n "Installing Python dependencies... " \
    && apk --no-cache add --virtual .python-deps \
      bzip2-dev \
      expat-dev \
      gdbm-dev \
      libffi-dev \
      ncurses-dev \
      openssl-dev \
      sqlite-dev \
      zlib-dev \
        >/dev/null 2>&1 \
  && echo "Done." \
  \
  # Install build dependencies. 
  #
  # - build-base, linux-headers: GCC toolchain (binutils, fortify-headers, g++, gcc, libc-dev, make) plus Linux headers for compile dependencies.
  # - coreutils: The basic file, shell and text manipulation utilities.
  # - findutils: GNU utilities for finding files.
  # - libnsl-dev: Network services library. 
  # - libtirpc-dev: Remote Procedure Call (RPC) library.
  # - pax-utils: ELF related utils for ELF 32/64 binaries.
  # - readline-dev: Utilities that allow users to edit command lines as they are typed.
  # - util-linux-dev: Random collection of Linux utilities.
  \ 
  && echo -n "Installing build dependencies... " \
    && apk --no-cache add --virtual .build-deps \
      build-base \
      coreutils \
      findutils \
      libnsl-dev \
      libtirpc-dev \
      linux-headers \
      pax-utils \
      readline-dev \
      util-linux-dev \
        >/dev/null 2>&1 \
    && echo "Done." \
  \  
  # Retrieve the source files.
  && echo -n "Downloading source... " \
    && wget -O python.tar.xz "https://www.python.org/ftp/python/${PYTHON_VERSION}/Python-${PYTHON_VERSION}.tar.xz" >/dev/null 2>&1 \
    && mkdir -p /usr/src/python \
    && tar -xJC /usr/src/python --strip-components=1 -f python.tar.xz >/dev/null 2>&1 \
    && rm python.tar.xz \
    && cd /usr/src/python \
    && echo "Done." \
  \
  # Configure the build.
  #  ./configure switches:
  #  --build: This switch specifies the target platform.
  #  --enable-optimisations: This switch enables Profile guided optimization (PGO) and Link Time Optimization (LTO). 
  #  --enable-shared: [Disabled]. This switch produces a Python binary that runs against .so libraries (and produces them at build time). LD_LIBRARY_PATH must be correctly set to use these.
  #  --enable-loadable-sqlite-extensions: This switch ensures to build the sqlite3 module. Required by iPython (plus many other things).
  #  --enable-ipv6: This switch ensures that the socket module supports IPv6.
  #  --with-system-ffi: Switch disabled for this platform. Enabled by default. Requires Requires installation of libffi-dev library via APK. Used to compile the _ctypes module. 
  #  --with-system-expat: This switch enables linking against the system version of Expat. Requires installation of expat-dev library via APK.
  #  --with-ensurepip: This switch enables building pip and setuptools packaging programs. 
  #  --without-dtrace: This switch disables DTrace support. 
  #
  #  C compiler flags (see https://gcc.gnu.org/onlinedocs/gcc/Optimize-Options.html#Optimize-Options)
  #  -Os: Optimise for disk space. Alternative option: -O2 (Optimize for nearly all supported optimizations that do not involve a space-speed tradeoff).
  #  -g0: Disable debug statements.
  #  -Wl,--strip-all: Remove symbol files.
  #  -DTHREAD_STACK_SIZE: bugfix.
  #
  && echo -n "Configuring build parameters... " \
    && ./configure \
      --prefix="$PYTHONHOME" \
      --build="x86_64-linux-musl" \
      --enable-optimizations \
      --enable-shared \
      --enable-loadable-sqlite-extensions \
      --enable-ipv6 \
      --with-ensurepip="install" \
      --with-system-expat \
      --without-dtrace \
        >/dev/null 2>&1 \
    && echo "Done." \
  \
  && echo -n "Compiling the application [this will take a while]... " \
    && make -j "$(nproc)" \
      EXTRA_CFLAGS="-Os -g0 -Wl,--strip-all -DTHREAD_STACK_SIZE=0x100000" \
        >/dev/null 2>&1 \
    && echo "Done." \
  \
  # Install to the prefix defined in the `./configure` step. (Default paths are executables in /usr/local/bin/, data files in /usr/local/share/.)
  # Use install rather than altinstall to overwrite any existing Python binary (which shouldn't exist anyway).
  && echo -n "Installing the application to ${PYTHONHOME}... " \
    && make install >/dev/null 2>&1 \
    && echo "Done." \
  \
  # Upgrade Pip
  && echo -n "Upgrading Pip and Setuptools... " \
    # Emulate the LD_LIBRARY_PATH with a symlink. If logging out/in (or spinning up a new image based on this one), this wouldn't have been necessary.
    && ln -sf "${PYTHONHOME}/lib/libpython3.7m.so.1.0" /usr/lib/libpython3.7m.so.1.0 \
    && "${PYTHONHOME}/bin/pip3" install --upgrade pip setuptools >/dev/null 2>&1 \
    && echo "Done." \
  \
  # Save a runtime dependencies list for use in the next build stage.
  && echo -n "Saving the runtime dependencies... " \
    && runDeps="$( \
        scanelf --needed --nobanner --recursive "$PYTHONHOME" \
            | awk '{ gsub(/,/, "\nso:", $2); print "so:" $2 }' \
            | sort -u \
            | xargs -r apk info --installed \
            | sort -u \
        )" \
    && echo "$runDeps" > "${PYTHONHOME}/run-dependencies.txt" \
    && echo "Done." \
  \
  && echo "Cleaning image of unnecessary files." \
    && if [ -n "$(find "$PYTHONHOME" -name "*.c")" ]; then echo -n "> Removing *.c artifacts... "; \
      find "$PYTHONHOME" -name "*.c" -delete && echo "Done.";  fi \
    \
    && if [ -n "$(find "$PYTHONHOME" -name "*.pxd")" ]; then echo -n "> Removing *.pxd artifacts... "; \
      find "$PYTHONHOME" -name "*.pxd" -delete && echo "Done.";  fi \
    \
    && if [ -n "$(find "$PYTHONHOME" -name "*.pyd")" ]; then echo -n "> Removing *.pyd artifacts... "; \
      find "$PYTHONHOME" -name "*.pyd" -delete && echo "Done."; fi \
    \
    && if [ -n "$(find "$PYTHONHOME" -regex "^.*\(__pycache__\|\.py[co]\)$")" ]; then echo -n "> Removing __pycache__ artifacts... "; \
      find "$PYTHONHOME" -regex "^.*\(__pycache__\|\.py[co]\)$" -delete && echo "Done."; fi \
    \
    && if [ -n "$(find "$PYTHONHOME" -type d -a \( -name test -o -name tests \))" ]; then echo -n "> Removing test[s] artifacts... "; \
      find "$PYTHONHOME" -type d -a \( -name test -o -name tests \) -exec rm -rf '{}' + && echo "Done."; fi \
    \
    && if [ -n "$(find "$PYTHONHOME" -type d -name "ensurepip")" ]; then echo -n "> Removing ensurepip... "; \
      find "$PYTHONHOME" -type d -name "ensurepip" -exec rm -rf '{}' + && echo "Done."; fi \
    \
    && if [ -n "$(find "$PYTHONHOME" -type d -name "idlelib")" ]; then echo -n "> Removing idlelib... "; \
      find "$PYTHONHOME" -type d -name "idlelib" -exec rm -rf '{}' + && echo "Done."; fi \
    \
    #&& echo -n "Uninstalling packages... " \
    #  Not necessary. Retained for future use or as required.
    #  && apk del .fetch-deps .python-deps .build-deps && echo "Done." \
  \
  && echo "Stage one (builder) complete!"

###########################################
# STAGE TWO (Production)
#
FROM alpine:3.9 as production
MAINTAINER Nicholas Laurent 0x666f6f@nym.hush.com
LABEL \
  IMAGE="0x666f6f/alpine-python3-minimal:optimised-3.7" \
  DISTRIBUTION="Alpine Linux 3.9.3" \
  PYTHON="3.7.3" \
  PIP="19.1"
ENTRYPOINT ["sh"]
CMD ["-c", "python"]
ENV \
  LANG="C.UTF-8" \
  PYTHONHOME="/usr/local" \
  PYTHONPATH="/usr/local/bin" \
  LD_LIBRARY_PATH="${LD_LIBRARY_PATH}:${PYTHONHOME}/lib" \
  C_INCLUDE_PATH="${C_INCLUDE_PATH}:${PYTHONHOME}/include"
COPY --from=builder "${PYTHONHOME}/bin" "${PYTHONHOME}/bin"
COPY --from=builder "${PYTHONHOME}/include" "${PYTHONHOME}/include"
COPY --from=builder "${PYTHONHOME}/lib" "${PYTHONHOME}/lib"
COPY --from=builder "${PYTHONHOME}/share" "${PYTHONHOME}/share"
COPY --from=builder "${PYTHONHOME}/run-dependencies.txt" /root/
RUN set -e \
  && echo -n "Installing packages... " \
    && cat /root/run-dependencies.txt | xargs -rt apk --no-cache add >/dev/null 2>&1 \
    && echo "Done." \
  \
  && echo -n "Creating symlinks... " \
    && if [ ! -e "/usr/bin/python" ]; then ln -sf "$(which python3)" /usr/bin/python; fi \
    && if [ ! -e "/usr/bin/pydoc" ]; then ln -sf "$(which pydoc3)" /usr/bin/pydoc; fi \
    && if [ ! -e "/usr/bin/python-config" ]; then ln -sf "$(which python3-config)" /usr/bin/python-config; fi \
    && if [ ! -e "/usr/bin/pip" ]; then ln -sf "$(which pip3)" /usr/bin/pip; fi \
    && echo "Done." \  
  \
  && echo "Stage two (production) complete!"
