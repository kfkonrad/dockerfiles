FROM alpine:3.10

RUN mkdir /fish-2.1.0
COPY *.patch /fish-2.1.0/
RUN apk add --no-cache bc curl g++ git groff libgcc libstdc++ make mdocml-apropos ncurses ncurses-dev sudo util-linux autoconf \
    && curl -Ls https://github.com/fish-shell/fish-shell/releases/download/2.1.0/fish-2.1.0.tar.gz | tar -xzf - \
    && cd fish-2.1.0 \
    && patch -p1 < 0001-Solaris-build-fixes-use-_sys_errs-if-available.patch \
    && ./configure \
    && make \
    && make install \
    && cd / \
    && rm -rf fish-2.1.0 \
    && apk del --no-cache g++ make ncurses-dev autoconf \
    && fish -c true \
    && adduser -D -u 1000 -s /usr/local/bin/fish nemo \
    && echo 'nemo ALL=(ALL) NOPASSWD: ALL' >> /etc/sudoers

USER nemo
WORKDIR /home/nemo

CMD ["fish"]
