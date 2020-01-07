FROM sironekotoro/alpine-perl

# /usrにMojoliciousをインストール
# alpine-perlで/usrにはパスが通っている
WORKDIR /usr
RUN cpm install Mojolicious

# 直近のファイルのみclone(--depth 1)
# gitの内容は/webappに展開
RUN git clone --depth 1 https://sironekotoro@bitbucket.org/sironekotoro/bbs_custom.git /webapp

# webappフォルダに移動
WORKDIR /webapp

# PlackでMojoliciousを起動
CMD plackup --port $PORT bbs_custom.pl