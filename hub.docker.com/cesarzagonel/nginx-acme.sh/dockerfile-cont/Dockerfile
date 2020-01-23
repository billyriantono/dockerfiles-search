FROM alpine

COPY /kernels /kernels
RUN chown -R 1000:100 /kernels
RUN find /kernels -type f -iname "*.sh" -exec chmod -v +x {} \;
RUN ls -la /kernels

ENTRYPOINT ["/bin/sh", "-c"]