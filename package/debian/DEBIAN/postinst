#!/bin/sh
set -e

# 服务名称（与 systemd 服务文件一致）
SERVICE="smartdns"

# 当包处于“配置”阶段（安装/更新时）执行
if [ "$1" = "configure" ]; then
    # 重新加载 systemd 配置（确保新服务文件生效）
    systemctl daemon-reload >/dev/null 2>&1 || true

    # 启用服务（创建自启动链接）
    systemctl enable "$SERVICE" >/dev/null 2>&1 || true

    # 如果服务已运行则重启，未运行则启动
    if systemctl is-active --quiet "$SERVICE"; then
        systemctl restart "$SERVICE" >/dev/null 2>&1 || true
    else
        systemctl start "$SERVICE" >/dev/null 2>&1 || true
    fi
fi

exit 0
