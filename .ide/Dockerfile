# .ide/Dockerfile

# 可将 node 替换为需要的基础镜像
FROM docker.cnb.cool/avwq/cnb.cool/cnb-avwq-default-dev-env-centos-stream:stream10

# 安装 code-server 和 vscode 常用插件
RUN curl -fsSL https://code-server.dev/install.sh | sh \
  && code-server --install-extension cnbcool.cnb-welcome \
  && code-server --install-extension redhat.vscode-yaml \
  && code-server --install-extension dbaeumer.vscode-eslint \
  && code-server --install-extension waderyan.gitblame \
  && code-server --install-extension mhutchie.git-graph \
  && code-server --install-extension donjayamanne.githistory \
  && code-server --install-extension tencent-cloud.coding-copilot \
  && echo done

# 安装 ssh 服务，用于支持 VSCode 等客户端通过 Remote-SSH 访问开发环境（也可按需安装其他软件）
RUN dnf update -y && dnf install -y git wget unzip openssh-server epel-release curl vim unzip procps && dnf install -y atop btop htop iftop iotop cockpit
# 业务安装
RUN dnf install -y nodejs npm python && dnf groupinstall "Development Tools" -y &&  dnf install -y libX11-devel.x86_64 libxkbfile-devel.x86_64 libsecret-devel krb5-devel && dnf install -y fakeroot rpm
RUN ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && echo "Asia/Shanghai" > /etc/timezone
RUN npm i -g pnpm



# 创建 `/ide_cnb` 目录，用于安装 IDE。系统通过此目录自动识别已安装的 IDE，安装路径必须为 `/ide_cnb`。
RUN mkdir -p /ide_cnb
# WebStorm
RUN wget https://download.jetbrains.com/webstorm/WebStorm-2026.1.tar.gz \
    && tar -zxvf WebStorm-2026.1.tar.gz -C /ide_cnb \
    && rm WebStorm-2026.1.tar.gz



# 指定字符集支持命令行输入中文（根据需要选择字符集）
ENV LANG C.UTF-8
ENV LANGUAGE C.UTF-8
