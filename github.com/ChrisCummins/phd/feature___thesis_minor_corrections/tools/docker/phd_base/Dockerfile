# Create a minimal Ubuntu environment for bazel-built binaries.
FROM python:3.6-slim
LABEL maintainer="Chris Cummins <chrisc.101@gmail.com>"

# Put Python into /bin, needed by bazel py_binary script entrypoints.
RUN ln -s /usr/local/bin/python3.6 /usr/bin/python && ln -s /usr/local/bin/python3.6 /usr/bin/python3

# Install a few necessary bits and pieces:
#   * a standard compiler toolchain which is needed for cldrive harnesses
#    (because the current clang compilation is not yet entirely hemetic and
#     relies on system linker and C headers)
#   * libreadline6-dev to provide libreadline.so which is needed by oclgrind.
#   * lbzip2 which is needed by tar to unpack .tar.bz2 files, which clgen
#     uses to encode corpus archives.
#   * git is needed by //third_party/py/git and my own tools.
#   * rsync is needed by a handful of targets, e.g. //system/machines.
#   * libexempi is required by //third_party/py/libxmp.
#   * ping is needed by //system/machines.
#   * rsync is needed by //system/machines.
#   * libmariadb3 is needed by //third_party/py/mysql
#   * python3-numpy because pip-installed build is broken, see:
#     https://github.com/numpy/numpy/issues/12977
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    binutils libgcc-7-dev libc6-dev libreadline6-dev lbzip2 git rsync \
    libexempi-dev iputils-ping rsync libmariadb3 python3-numpy \
    && rm -rf /var/lib/apt/lists/*

# Dirty hack to workaround the fact that oclgrind demands libreadline.so.6, but
# the current Ubuntu package provides libreadline.so.7.
RUN ln -s /lib/x86_64-linux-gnu/libreadline.so.7 \
    /lib/x86_64-linux-gnu/libreadline.so.6

# Install libmysql.so needed by //third_party/py/sqlalchemy.
RUN apt-get update \
  && apt-get install -y --no-install-recommends mysql-common wget \
  && wget http://launchpadlibrarian.net/407536926/libmysqlclient20_5.7.25-0ubuntu0.16.04.2_amd64.deb \
  && dpkg -i libmysqlclient20_5.7.25-0ubuntu0.16.04.2_amd64.deb \
  && rm libmysqlclient20_5.7.25-0ubuntu0.16.04.2_amd64.deb \
  && apt-get remove -y wget \
  && rm -rf /var/lib/apt/lists/*

# Remove unneeded files to reduce the image size.
RUN rm -rf /usr/share/doc

# Create a non-root user to execute commands with. This is so that generated
# files in mapped volumes will be created as this user, rather than as root.
RUN useradd -ms /bin/bash docker
# Add docker to a 'other_docker' group, which enables read permission when
# mapping /var/run/docker.sock to enable nested docker.
RUN groupadd --gid 123 other_docker && usermod -a -G other_docker docker
USER docker

ENTRYPOINT ["/bin/bash"]
