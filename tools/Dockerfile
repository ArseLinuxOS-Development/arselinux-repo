FROM archlinux
RUN pacman -Syu --noconfirm base-devel && useradd -m -G wheel builder && echo "builder ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers
USER builder
WORKDIR /build
ENTRYPOINT ["makepkg", "-sf", "--noconfirm"]

