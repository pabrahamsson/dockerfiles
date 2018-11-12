FROM fedora:29
MAINTAINER petter@jebus.nu
LABEL RUN='docker run --rm -it --name franz -v /home/${USER}:/home/franz -v /tmp/.X11-unix:/tmp/.X11-unix -e DISPLAY=${DISPLAY} --device /dev/snd -e PULSE_SERVER=unix:${XDG_RUNTIME_DIR}/pulse/native -v ${XDG_RUNTIME_DIR}/pulse/native:${XDG_RUNTIME_DIR}/pulse/native --group-add $(getent group audio | cut -d: -f3) --security-opt label=type:container_runtime_t quay.io/pabrahamsson/franz'
RUN INSTALL_PKGS="alsa-utils pulseaudio nss GConf2 libXScrnSaver libcanberra-gtk2" && \
    dnf install -y $INSTALL_PKGS && \
    dnf clean all && \
    export uid=1000 gid=1000 && \
    mkdir -p /home/franz/.config/Franz && \
    curl -Lo /tmp/franz.tar.gz https://github.com/meetfranz/franz/releases/download/v5.0.0-beta.18/franz-5.0.0-beta.18.tar.gz && \
    tar zxvf /tmp/franz.tar.gz -C /usr/local/bin --strip-components=1 && \
    rm -f /tmp/franz.tar.gz && \
    echo "franz:x:${uid}:${gid}:Meet Franz,,,:/home/franz:/bin/bash" >> /etc/passwd && \
    echo "franz:x:${uid}:" >> /etc/group && \
    chown ${uid}:${gid} -R /home/franz && \
    usermod -a -G audio franz

USER franz
ENV HOME /home/franz
ENV LANG en_US.UTF-8
ENV TERM xterm-256color
WORKDIR /home/franz
ENTRYPOINT [ "/usr/local/bin/franz" ]
