FROM huggla/alpine as alpine
ARG TARFILES="rootfs.tar etc-apt.tar"
COPY ./*.tar /tmp/
RUN exec 2>&1 \
 && set -x \
 && cd /tmp \
 && for tarfile in ${TARFILES}; do tar x -pf "$tarfile"; done \
 && rm -f ${TARFILES} \
 && apk --no-cache add gnupg \
 && wget -O - "https://keyserver.ubuntu.com/pks/lookup?op=get&search=0xa1715d88e1df1f24" | gpg --import \
 && gpg --no-default-keyring --export --armor a1715d88e1df1f24 > /tmp/etc/apt/trusted.gpg.d/git.asc \
 && echo "deb http://ppa.launchpad.net/git-core/ppa/ubuntu xenial main" >> /tmp/etc/apt/sources.list

FROM scratch
LABEL org.label-schema.vendor="Blitznote" \
      org.label-schema.build-date="2017-12-01T00:00:00+00:00" \
      org.label-schema.name="minimal base images with Ubuntu" \
      org.label-schema.vcs-type="git" \
      org.label-schema.vcs-url="https://github.com/Blitznote/debase" \
      org.label-schema.schema-version="1.0rc1" \
      operatingsystem="linux" \
      kernelversion="4.10.0" \
      minkernelversion="4.4.0" \
      arch="amd64" \
      subarch="cx16 fxsr pclmul popcnt mmx sse2 sse3 ssse3 sse4_1 sse4_2" \
      family="haswell silvermont excavator zx-c" \
      minfamily="ivybridge silvermont piledriver zx-c"

COPY --from=alpine /tmp /
CMD ["/bin/bash"]
SHELL ["/bin/bash", "-c"]
