# let's start from a common base, already 'apt-ed'
FROM pinver/ldc_lin:1.7.0

# in only one layer, what is needed by ...
RUN apt-get update && apt-get install -y \
    wget `# to download` \
    software-properties-common `# ` && \
    wget -O - http://apt.llvm.org/llvm-snapshot.gpg.key | apt-key add - && \
    apt-add-repository "deb http://apt.llvm.org/xenial/ llvm-toolchain-xenial-6.0 main" && \
    apt-get update && apt-get install -y lld-6.0 

ADD lib/v1.7.0 /root/dlang/ldc-1.7.0/lib_win

CMD ["bash"]
