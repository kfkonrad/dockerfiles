FROM alpine:3.21.2

ARG  FISH_VERSION=3.1.2

RUN echo "Building Fish-${FISH_VERSION}"; \
    apk update \
    && apk add curl \
    && curl \
        --location \
        --silent \
    https://github.com/fish-shell/fish-shell/releases/download/${FISH_VERSION}/fish-${FISH_VERSION}.tar.gz \
    | tar -xzf -
RUN apk add \
        bash \
        bc \
        cmake \
        g++ \
        git \
        groff \
        less \
        libgcc \
        libstdc++ \
        make \
        mandoc-apropos \
        ncurses \
        ncurses-dev \
        openssh-client \
        python3 \
        screen \
        sed \
        sudo \
        util-linux \
        vim
RUN cd fish-${FISH_VERSION} \
    && make build \
    && cd build \
    && cmake .. \
    && make \
    && make install
RUN fish -c true \
    && adduser \
        -D \
        -u 1000 \
        -s /usr/local/bin/fish \
        nemo \
    && echo 'nemo ALL=(ALL) NOPASSWD: ALL' >> /etc/sudoers

USER nemo
WORKDIR /home/nemo

CMD ["fish"]
