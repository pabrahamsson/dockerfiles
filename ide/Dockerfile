FROM fedora:28
MAINTAINER petter@jebus.nu
LABEL RUN='docker run -it --rm --name vim -w $(pwd|sed "s/$(whoami)/developer/") --cpus 0.3 -m 32 -v /home/${USER}:/home/developer -v /tmp/.X11-unix:/tmp/.X11-unix -e DISPLAY=${DISPLAY} --security-opt label=type:container_runtime_t quay.io/pabrahamsson/vim'
RUN dnf install -y git zsh tmux && \
    BUILD_DEPS=$(dnf groups install -y 'Development Tools'|grep Installing|awk '{print $3}') && \
    DEPS=$(dnf install -y ncurses-devel|grep Installing|awk '{print $3}') && \
    git clone https://github.com/vim/vim && \
    cd vim/src && \
    ./configure --with-tlib=ncurses --exec-prefix=/ && \
    make && make install && \
    cd ../../ && rm -rf vim && \
    dnf remove -y $BUILD_DEPS $DEPS && \
    dnf clean all && \
    export uid=1000 gid=1000 && \
    mkdir -p /home/developer && \
    echo "developer:x:${uid}:${gid}:Developer,,,:/home/developer:/bin/zsh" >> /etc/passwd && \
    echo "developer:x:${uid}:" >> /etc/group && \
    chown ${uid}:${gid} -R /home/developer

USER developer
ENV HOME /home/developer
ENV LANG en_US.UTF-8
ENV TERM xterm-256color
WORKDIR /home/developer
ENTRYPOINT ["vim"]
