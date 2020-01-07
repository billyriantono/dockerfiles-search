FROM centos:6.7

MAINTAINER RCVN nguyen.tuankhanh@rivercrane.vn

# Set Timezone Asia/Ho_Chi_Minh
RUN echo "Asia/Ho_Chi_Minh" > /etc/timezone
RUN rm -f /etc/localtime
RUN ln -sf /usr/share/zoneinfo/Asia/Ho_Chi_Minh  /etc/localtime