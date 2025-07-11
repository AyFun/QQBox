# QQ Docker (Linux QQ for WSL2)

> **Note:** 本项目仅在 Windows 11 的 WSL2 (Debian) 上测试，其他平台请自行修改和适配。


## 项目特色

- 保护文件隐私
- 解决高分辨率缩放模糊问题
- 解决缩放后鼠标大小异常问题

## 启动命令

```bash
# 在 WSL2 中启动 QQ 容器
wsl docker run -tid \
  --rm \                                           # 容器停止时自动删除
  --name qqbox \                                   # 容器名称
  --shm-size="1g" \                                # 设置共享内存大小，避免卡顿
  -e DISPLAY=$DISPLAY \                            # 转发 X11 显示
  -e WAYLAND_DISPLAY=$WAYLAND_DISPLAY \            # 转发 Wayland 显示
  -e XDG_RUNTIME_DIR=$XDG_RUNTIME_DIR \            # 转发用户运行时目录
  -v /tmp/.X11-unix:/tmp/.X11-unix \               # 挂载 X11 套接字
  -v /mnt/wslg:/mnt/wslg \                         # 挂载 WSLg 目录（支持音频、图形等）
  -v /usr/lib/wsl/lib:/usr/lib/wsl/lib \           # 挂载 WSL 库
  -v /mnt/c/Windows/Fonts:/usr/share/fonts/win11 \ # 挂载 Windows 字体
  -v /mnt/d/QQ:/root/.config/QQ \                  # 挂载 QQ 目录到D:\QQ
  -v /mnt/d/QQfiles:/root/QQfiles \                # 挂载 QQ 文件目录到D:\QQfiles
  qqbox:latest
```


## 高分屏适配

如果在高分辨率环境中需要缩放，请将 `.wslgconfig` 文件放到 `%USERPROFILE%` 下，例如：

```
C:\Users\<你的用户名>\.wslgconfig
```
