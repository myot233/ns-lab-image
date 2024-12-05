FROM debian:12-slim
COPY noVNC noVNC
EXPOSE 6080
EXPOSE 5901
WORKDIR /
ARG ROOT_PASSWORD="123456"
ARG VNC_PASSWORD="123456"

# 使用ustc源
RUN rm -f /etc/apt/sources.list.d/debian.sources && \
    echo "deb http://mirrors.ustc.edu.cn/debian bookworm main" > /etc/apt/sources.list && \
    echo "deb http://mirrors.ustc.edu.cn/debian bookworm-updates main" >> /etc/apt/sources.list && \
    echo "deb http://mirrors.ustc.edu.cn/debian-security bookworm-security main" >> /etc/apt/sources.list

# 安装包
RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y \
    python3 \
    tigervnc-standalone-server \
    bash \
    nginx \
    supervisor \
    xfce4 \
    xfce4-terminal \
    dbus-x11 \
    lightdm-gtk-greeter && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*
RUN rm -f /etc/nginx/sites-enabled/default

RUN echo "root:${ROOT_PASSWORD}" | chpasswd
RUN mkdir -p /root/.vnc && \
    echo "${VNC_PASSWORD}" | vncpasswd -f > /root/.vnc/passwd && \
    chmod 600 /root/.vnc/passwd

COPY supervisor.conf /etc/supervisor/conf.d/supervisord.conf
COPY nginx.conf /etc/nginx/conf.d/default.conf
ENTRYPOINT ["supervisord", "-n"]



