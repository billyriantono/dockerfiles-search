FROM brsynth/rpcache

RUN conda install -c conda-forge flask-restful

ONBUILD COPY rpTool.py /home/
ONBUILD COPY rpToolServe.py /home/
ONBUILD COPY rpToolCache.py /home/
ONBUILD RUN rm -f /home/Dockerfile

ONBUILD ENTRYPOINT ["python"]
ONBUILD CMD ["/home/rpToolServe.py"]

# Open server port
ONBUILD EXPOSE 8888
