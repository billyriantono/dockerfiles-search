FROM srcml/fedora_x86_64_base:26

WORKDIR /srcML-build

CMD ["/bin/bash", \
     "-c", \
      "cmake -DBUILD_CLIENT_TESTS=ON -DBUILD_UNIT_TESTS=OFF -DBUILD_TIMING_TESTS=OFF /srcML; \
      make install; \
      ldconfig; \
      ctest -VV -D Nightly -T MemCheck --overwrite Site='fedora_26_x86_64-client' "]
