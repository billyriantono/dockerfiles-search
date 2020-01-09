# Run RStudio in a container
#
# docker run -it \
#   -v /tmp/.X11-unix:/tmp/.X11-unix \ # mount the X11 socket
#   -e DISPLAY=unix$DISPLAY \
#   -v $HOME/rscripts:/root/rscripts \
#   --device /dev/dri \
#   --name rstudio \
#   jess/rsudio
#
FROM jess/rstudio

# Autorun Rstudio
# ENTRYPOINT [ "rstudio" ]
