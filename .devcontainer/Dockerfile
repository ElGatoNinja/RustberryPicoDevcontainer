# See here for image contents: https://github.com/microsoft/vscode-dev-containers/tree/v0.238.0/containers/rust/.devcontainer/base.Dockerfile

# [Choice] Debian OS version (use bullseye on local arm64/Apple Silicon): buster, bullseye
ARG VARIANT="buster"
FROM mcr.microsoft.com/vscode/devcontainers/rust:0-${VARIANT}

#debugger support
RUN apt-get update && \ 
    apt-get install -y --no-install-recommends \
    git gdb-multiarch \
    openocd \
    minicom

#usbip support (allow to connect to a usb in a windows host)
RUN apt-get update && apt-get -y --no-install-recommends install usbip

RUN rustup self update && rustup update stable
RUN rustup target add thumbv6m-none-eabi

