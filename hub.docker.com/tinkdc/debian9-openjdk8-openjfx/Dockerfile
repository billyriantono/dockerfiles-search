FROM openjdk:8

ENV TZ=Asia/Shanghai
ENV LANG zh_CN.UTF-8
ENV LANGUAGE zh_CN:zh
ENV LC_ALL zh_CN.UTF-8

RUN apt update \
    && apt install openjdk-8-jdk openjfx locales -y \ 
    && ln -sf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone \
    && locale-gen --purge en_US.UTF-8 zh_CN.UTF-8 \ 
    && localedef -i zh_CN -c -f UTF-8 -A /usr/share/locale/locale.alias zh_CN.UTF-8 \
    &&  echo 'LANG="zh_CN.UTF-8"' > /etc/default/locale &&  echo 'LANGUAGE="zh_CN.UTF-8"' >> /etc/default/locale  && echo "export LANG=zh_CN.utf8" >> ~/.bash_profile 

CMD ["bash"]
