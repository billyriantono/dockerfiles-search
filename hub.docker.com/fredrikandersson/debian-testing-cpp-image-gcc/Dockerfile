# Docker image for C++ development using GCC, based on base C++ image for Debian testing.

FROM fredrikandersson/debian-testing-cpp-image-base:testing-2019-09-10

# We don't want to mix with gcc/stdlibc++ ver. 4
RUN apt-get remove gcc --quiet --yes
RUN apt-get autoremove --quiet --yes

RUN apt-get update --quiet --yes && apt-get install --quiet --yes g++5 ccache
