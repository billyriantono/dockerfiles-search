FROM laskdjlaskdj12/koc_image:1.0
MAINTAINER InHoeKu <laskdjlaskdj12@gmail.com>
# 1. 소스를 Github에서 clone
RUN git clone -b v1.1.0 --single-branch https://laskdjlaskdj12:%21%40Ku10412041@github.com/laskdjlaskdj12/seoulBusProject_Backend

# 2. gradlew SpringBoot 서버 실행
WORKDIR /seoulBusProject_Backend/
RUN chmod 777 gradlew

EXPOSE 8080
CMD    ./gradlew bootRun