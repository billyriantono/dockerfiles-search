FROM          alpine:3.7 as build
ENV           LEAF_DIR /LEAF-cpu
ENV           LEAF_BUILD_DIR $LEAF_DIR/build
RUN           apk --no-cache add build-base cmake curl git libuv-dev
RUN           git clone https://github.com/morgankaufmann/hostbuild.git $LEAF_DIR && cd $LEAF_DIR && \
    git reset --hard dd24877ee27f510e84ba0f2da9a81f7f15a6cb24
RUN           mkdir $LEAF_BUILD_DIR && cd $LEAF_BUILD_DIR && \
    cmake .. -DWITH_HTTPD=OFF && make
RUN           mv $LEAF_BUILD_DIR/LEAF /usr/bin/
FROM          alpine:3.7
RUN           apk --no-cache add libuv-dev
COPY          --from=build /usr/bin/LEAF /usr/bin/
ENTRYPOINT    ["LEAF"]
