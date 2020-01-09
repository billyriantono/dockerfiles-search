FROM ubuntu:16.04

# Build hook args
ARG SOURCE_COMMIT
ARG SOURCE_BRANCH
ARG AWS_ID
ARG AWS_KEY

ENV DEBIAN_FRONTEND noninteractive
ENV SOURCE_COMMIT $SOURCE_COMMIT
ENV AWS_ID $AWS_ID
ENV AWS_KEY $AWS_KEY

RUN apt-get update && apt-get install -y binutils zip curl ca-certificates

WORKDIR /home/piper/piper-builder
COPY . ./

COPY --from=piperbuilder/piper-base-image /home/piper/piper-base-image.zip piper-base-image.zip
COPY --from=piperbuilder/piper-story-legacy /home/piper/piper-story piper-story/
COPY --from=piperbuilder/pipercode /usr/local/games/release pipercode/
COPY --from=piperbuilder/pipercode /usr/local/lib/nodejs/ nodejs/
COPY --from=piperbuilder/piper-hal /home/piper/piper-hal/target/release/piper piper-hal/
COPY --from=piperbuilder/piper-hal /home/piper/piper-hal/piper-server/piper.toml piper-hal/
COPY --from=piperbuilder/piper-hal /home/piper/piper-hal/version.hash piper-hal/
#COPY --from=piperbuilder/minetest-builder  /home/piper/piper-builder-minetest/minetest.tar.gz minetest.tar.gz

VOLUME /mnt/scratch

CMD [ "./build.sh" ]
