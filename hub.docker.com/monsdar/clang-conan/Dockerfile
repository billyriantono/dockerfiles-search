FROM conanio/clang8

RUN sudo apt-get -qq update \
    && sudo apt-get install -y --no-install-recommends \
    clang-tidy-8 \
    clang-format-8 \
    vim \
    nano \
    && sudo apt-get clean

VOLUME [/source]

COPY build.sh /build/
CMD ["/build/build.sh"]
