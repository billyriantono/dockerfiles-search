FROM sequenceiq/hadoop-docker:2.7.0

WORKDIR /usr/local/hadoop/workspace

COPY src .

RUN echo "export PATH=$PATH:/usr/local/hadoop/bin" >> ~/.bashrc
RUN echo "export HADOOP_LIB=/usr/local/hadoop-2.7.0/share/hadoop/tools/lib" >> ~/.bashrc

CMD ["/etc/bootstrap.sh","-bash"]
