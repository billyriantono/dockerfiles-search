FROM centos:7.3.1611

WORKDIR /root/

 # 安装编译vim的依赖库
RUN yum -y install epel-release \
 && yum -y install python36 python36-devel \
    lua lua-devel ncurses-devel gcc gcc-c++ ctags cscope \
    wget unzip cmake make git \
 # 建立python3软链接
 && ln -s /usr/bin/python36 /usr/bin/python3 \
 # 安装pip3
 && curl "https://bootstrap.pypa.io/get-pip.py" -o "get-pip.py" \
 && python3 get-pip.py \
 # 下载编译源码
 && wget https://github.com/vim/vim/archive/master.zip \
 && unzip master.zip && cd vim-master \
 && ./configure --with-features=huge \
        --enable-rubyinterp \
        --enable-luainterp \
        --enable-python3interp=yes \
        --enable-pythoninterp=yes \
 && make && make install \

 # pip3 安装python补全和语法检查引擎
 && pip3 install jedi flake8 \
 # 安装vimPlug和相关配置
 && curl -fLo ~/.vim/autoload/plug.vim --create-dirs \
    https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim \
 && rm /root/* -rf \
 # 修改字符集
 && localedef -c -f UTF-8 -i zh_CN zh_CN.utf8 \
 && echo "export LC_ALL=zh_CN.UTF-8" > /root/.bashrc \
 && echo "export LANG=zh_CN.UTF-8" > /root/.bashrc \
 && source /root/.bashrc

ENV LC_ALL zh_CN.UTF-8
ENV LANG   zh_CN.UTF-8
