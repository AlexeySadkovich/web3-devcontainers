FROM --platform=linux/amd64 mcr.microsoft.com/devcontainers/rust:1-bullseye

ARG SOLANA_RELEASE

WORKDIR /usr

RUN apt-get update -y && apt-get upgrade -y && apt-get install -y \
    pkg-config \
    build-essential \
    libudev-dev \
    libssl-dev

# Install nodejs
RUN curl -sL https://deb.nodesource.com/setup_12.x | bash - 
RUN apt-get install -y nodejs

RUN npm install -g typescript

# Install solana
RUN curl -LJO https://github.com/solana-labs/solana/releases/download/${SOLANA_RELEASE}/solana-release-x86_64-unknown-linux-gnu.tar.bz2
RUN tar jxf solana-release-x86_64-unknown-linux-gnu.tar.bz2
RUN cd solana-release && export PATH=$PWD/bin:$PATH
ENV PATH $PATH:/usr/solana-release/bin

# Install anchor
RUN sudo chown -R $(whoami) /usr/local/cargo/
RUN rustup toolchain install nightly
RUN cargo +nightly install -Z sparse-registry --git https://github.com/coral-xyz/anchor --tag v0.25.0 anchor-cli --locked


