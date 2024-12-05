
FROM alpine:3.20.3
COPY noVNC noVNC
EXPOSE 6080
EXPOSE 5901
WORKDIR /
ARG ROOT_PASSWORD="123456"
ARG VNC_PASSWORD="123456"

# 使用ustc源
RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.ustc.edu.cn/g' /etc/apk/repositories
# 安装包
RUN ["apk", "update"]
RUN ["apk","add","python3","tigervnc","bash","nginx","supervisor","xfce4", "xfce4-terminal", "xfce4-screensaver", "lightdm-gtk-greeter"]


RUN echo "root:${ROOT_PASSWORD}" | chpasswd
RUN echo -e "${VNC_PASSWORD}\n${VNC_PASSWORD}\nn" | vncpasswd

COPY supervisor.conf /etc/supervisor.d/default.ini
COPY nginx.conf /etc/nginx/http.d/default.conf
ENTRYPOINT ["supervisord","-n"]



