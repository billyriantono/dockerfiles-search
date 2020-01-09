FROM timiil/firefly-rockchip-builder-root
LABEL maintainer "timiil <timiil@163.com>"

RUN cd /src && \
    repo init --repo-url https://github.com/FireflyTeam/repo.git -u https://github.com/FireflyTeam/manifests.git -b linux-sdk -m rk3328/rk3328_linux_release.xml && \
    repo sync -c
