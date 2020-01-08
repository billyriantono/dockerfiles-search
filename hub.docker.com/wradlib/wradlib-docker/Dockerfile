FROM wradlib/wradlib-docker:full

MAINTAINER wradlib <wradlib@wradlib.org>

USER root

# Install additional training dependencies
RUN source activate wradlib && \
    conda install --yes opencv \
    pandas \
    scikit-image && \
    conda clean -tipy

EXPOSE 8888 8889

COPY entrypoint.sh /usr/local/bin/entrypoint.sh
RUN chmod +x /usr/local/bin/entrypoint.sh
ENTRYPOINT ["/usr/local/bin/entrypoint.sh"]
CMD ["/bin/bash"]
