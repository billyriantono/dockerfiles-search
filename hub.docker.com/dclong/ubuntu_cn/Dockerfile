FROM dclong/ubuntu_b

# locale
RUN apt-get update \
    # && DEBIAN_FRONTEND=noninteractive apt-get install -y locales \
    && locale-gen zh_CN.UTF-8 \
    && apt-get autoremove \
    && apt-get autoclean
    
# ENV LANG=zh_CN.UTF-8 LANGUAGE=zh_CN:zh LC_ALL=zh_CN.UTF-8 