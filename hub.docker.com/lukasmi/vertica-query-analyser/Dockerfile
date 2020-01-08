FROM fpco/stack-build:lts-10.4 as build

ARG BUILD_PATH=/opt/build
RUN mkdir $BUILD_PATH
COPY . $BUILD_PATH
RUN cd $BUILD_PATH && stack build

FROM ubuntu:18.04

ARG APP_PATH=/opt/app
WORKDIR $APP_PATH

COPY --from=build /opt/build/.stack-work/install/x86_64-linux/lts-10.4/8.2.2/bin .

ENTRYPOINT ["./vq-analyser"]
