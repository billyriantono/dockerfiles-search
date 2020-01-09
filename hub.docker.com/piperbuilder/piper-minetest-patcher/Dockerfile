FROM piperbuilder/ubuntu-builder
ENV DEBIAN_FRONTEND noninteractive
WORKDIR /home/piper
COPY . piper-builder/piper2
WORKDIR piper-builder/piper2
COPY --from=piperbuilder/minetest-builder /home/piper/piper-builder-minetest/minetest.tar.gz minetest.tar.gz
VOLUME /mnt/scratch
CMD [ "./make-minetest-image.sh" ]
