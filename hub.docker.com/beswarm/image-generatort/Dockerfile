FROM plugins/docker
COPY ./authinit.sh /bin/
RUN chmod 777 /bin/authinit.sh
ENTRYPOINT ["/bin/authinit.sh", "/bin/drone-docker"]
