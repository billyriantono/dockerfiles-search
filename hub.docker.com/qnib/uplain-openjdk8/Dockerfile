FROM qnib/uplain-init

RUN apt-get update \
 && apt-get install -y locales openjdk-8-jdk-headless \
 && update-locale LANG=C.UTF-8 LC_MESSAGES=POSIX \
 && locale-gen en_US.UTF-8 \
 && dpkg-reconfigure locales \
 && apt-get clean all \
 && rm -rf /var/lib/apt/lists/* \
 && javac -version
