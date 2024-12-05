FROM gsycl2004/iis_experiment:debian-base

# 安装依赖
RUN apt-get update && apt-get install -y \
    python3-pip \
    python3-venv \
    firefox-esr \
    && rm -rf /var/lib/apt/lists/*

# 配置pip使用清华源
RUN pip config set global.index-url https://mirrors.tuna.tsinghua.edu.cn/pypi/web/simple

# 创建并激活虚拟环境
RUN python3 -m venv /opt/venv
ENV PATH="/opt/venv/bin:$PATH"

# 升级pip并安装依赖
RUN pip install --no-cache-dir \
    secretflow-lite \
    jupyter

RUN apt-get update && apt-get install -y fonts-noto-cjk python3-numpy
RUN echo 'export PATH="/opt/venv/bin:$PATH"' >> /root/.bashrc

COPY cic1.csv /root/Desktop/cic1.csv
COPY cic2.csv /root/Desktop/cic2.csv







