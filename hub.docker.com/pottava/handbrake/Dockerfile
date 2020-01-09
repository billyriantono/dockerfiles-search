# HandBrake CLI v1.2
# @see https://handbrake.fr/docs/en/latest/cli/cli-options.html
#
# docker run --rm pottava/handbrake:1.2
# docker run --rm -v $(pwd):/work pottava/handbrake:1.2 -i VIDEO_TS -o out.mp4

FROM ubuntu:cosmic-20190418

ENV DEBIAN_FRONTEND=noninteractive \
    HANDBRAKE_VERSION='1:1.2.1'

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
       "software-properties-common=0.96.27.1" \
       "libdvd-pkg=1.4.2-1-1" \
    && dpkg-reconfigure libdvd-pkg \
    && add-apt-repository -y ppa:stebbins/handbrake-releases \
    && apt-get update \
    && apt-get install -y --no-install-recommends \
       "handbrake-cli=${HANDBRAKE_VERSION}-zhb-1ppa1~cosmic1" \
    && apt-get remove -y --purge software-properties-common \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* \
       /var/cache/man /usr/src/libdvd-pkg \
    && find / -depth -type d -name __pycache__ -exec rm -rf {} \;

WORKDIR /work

ENTRYPOINT ["HandBrakeCLI"]
CMD ["--help"]
