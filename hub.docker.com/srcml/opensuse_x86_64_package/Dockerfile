FROM srcml/opensuse_x86_64_base:15.1

RUN zypper ref && zypper --non-interactive install --no-recommends rpm-build

CMD ["/bin/bash", \
     "-c", \
     "mkdir /srcML-build; \
      cd /srcML-build; \
      cmake /srcML; \
      make -j2; \
      cpack; \
      cpack -G RPM; \
      mv dist/srcML*.tar.gz /srcML_builds/opensuse_15.1_x86_64.tar.gz; \
      mv dist/srcML*.rpm /srcML_builds/opensuse_15.1_x86_64.rpm "]
