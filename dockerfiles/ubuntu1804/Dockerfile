FROM --platform=linux/386 ubuntu:18.04

ENV DEBIAN_FRONTEND=noninteractive


RUN sed -i \
    -e 's|http://archive.ubuntu.com/ubuntu|http://old-releases.archive.ubuntu.com/ubuntu|g' \
    -e 's|http://security.ubuntu.com/ubuntu|http://old-releases.archive.ubuntu.com/ubuntu|g' \
    -e 's|http://ports.ubuntu.com/ubuntu-ports|http://old-releases.archive.ubuntu.com/ubuntu|g' \
    /etc/apt/sources.list

RUN apt-get update && apt-get install -y \
    bash \
    dbus-x11 \
    xserver-xorg-core \
    xinit \
    x11-xserver-utils \
    x11-utils \
    x11-xserver-utils \
    lightdm \
    i3 \
    xterm \
    xfonts-base \
    fonts-dejavu-core \
    feh \
    xpdf \
    vim \
    nano \
    python3 \
    nodejs \
    gcc \
    openssh-client \
    && rm -rf /var/lib/apt/lists/*


RUN useradd -m -s /bin/bash user \
    && echo 'user:password' | chpasswd


RUN mkdir -p /home/user/.config/i3 \
    && printf 'exec xterm\n' > /home/user/.config/i3/config \
    && chown -R user:user /home/user/.config


RUN mkdir -p /etc/lightdm/lightdm.conf.d \
    && printf '[Seat:*]\nautologin-user=user\nautologin-user-timeout=0\nuser-session=i3\n' \
       > /etc/lightdm/lightdm.conf.d/50-webvm.conf

CMD ["/bin/bash"]
