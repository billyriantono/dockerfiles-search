FROM tensorflow/tensorflow

RUN apt-get update \
    && curl -sL https://deb.nodesource.com/setup_6.x | bash - \
    && apt-get install -y nodejs

RUN npm install -g ijavascript \
    && ijsinstall --hide-undefined --install=global

RUN cd /notebooks \
    && npm install dstools

# TensorBoard
EXPOSE 6006
# IPython
EXPOSE 8888

WORKDIR "/notebooks"

CMD ["/run_jupyter.sh", "--allow-root"]
