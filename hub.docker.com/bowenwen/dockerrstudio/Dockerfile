FROM rocker/geospatial:3.6.1

LABEL maintainer="Bo Wen <bo.wen@translink.ca>"

# install mssql related drivers and packages
RUN install2.r --error --deps TRUE cancensus rjson leafsync


## Notes ##
# other Dockerfile commands:
# EXPOSE <port> [<port>/<protocol>...]
# ENV <key>=<value> ...
# COPY [--chown=<user>:<group>] ["<src>",... "<dest>"] ## Copy from from host to Docker image
# ADD [--chown=<user>:<group>] ["<src>",... "<dest>"] ## COPY plus allows TAR file extract, and URL (RUN curl is preferred over ADD url)
# CMD ["executable","param1","param2"] ## default command, can be override
# ENTRYPOINT ["executable", "param1", "param2"] ## Exec form: cannot be override on run, always used (preferred over Shell form)
# ENTRYPOINT command param1 param2 ## Shell form: ignores any CMD or docker run

# check out rocker's rstudio image Dockerfile here:
# https://github.com/rocker-org/rocker-versioned/blob/master/rstudio/Dockerfile
# read more on Dockerfile: 
# https://docs.docker.com/engine/reference/builder/
# https://goinbigdata.com/docker-run-vs-cmd-vs-entrypoint/
