FROM mathnotes/sage:2019-08-22
MAINTAINER Ryan Jensen <ryan.jensen@mathnotes.cc>

## So it doesn't have to be built on mybinder.org
## Runtime configuration
USER $MN_USER
WORKDIR $MN_HOME

CMD jupyter notebook \
  --no-browser \
  --ip=* \
  --port=8888 \
  --NotebookApp.token='' \
  --NotebookApp.password=''

## Expose ports
EXPOSE 8888
