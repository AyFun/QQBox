FROM debian:12-slim

RUN sed -i 's/deb.debian.org/mirrors.cloud.tencent.com/g' /etc/apt/sources.list.d/debian.sources \
&& apt -y update && apt -y install wget libasound2 libglib2.0-bin dbus-x11 && cd ~ \
&& wget -O qq.deb https://dldir1v6.qq.com/qqfile/qq/QQNT/Linux/QQ_3.2.18_250616_amd64_01.deb \
&& apt install -y ./qq.deb \
&& apt-get autoclean && apt-get clean \
&& rm -rf /root/.config/QQ/* && rm -rf /tmp/* \
&& echo "Xcursor.size: 12" > ~/.Xresources

ENV ELECTRON_OZONE_PLATFORM_HINT=wayland
ENV LD_LIBRARY_PATH=/usr/lib/wsl/lib
VOLUME ["/root/.config/QQ"]

CMD ["dbus-run-session", "--", "sh", "-c", "\
    xrdb -load $HOME/.Xresources 2>/dev/null; \
    gsettings set org.gnome.desktop.interface cursor-size 12 2>/dev/null; \
    exec /opt/QQ/qq --no-sandbox --disable-gpu --disable-software-rasterizer --enable-unsafe-swiftshader\
"]