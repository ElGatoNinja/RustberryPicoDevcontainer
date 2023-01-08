FROM ubuntu:latest

SHELL ["bin/bash", "-c"]

#debugger support
RUN apt-get update && \ 
    apt-get install -y --no-install-recommends \
    build-essential \
    libudev-dev \
    pkg-config \
    git gdb-multiarch \
    openocd \
    minicom \
    curl \
    ca-certificates

ARG USERNAME=pico-dev
ARG USER_UID=1000
ARG USER_GID=$USER_UID

# Create the user
RUN groupadd --gid $USER_GID $USERNAME \
    && useradd --uid $USER_UID --gid $USER_GID -m $USERNAME \
    && apt-get update \
    && apt-get install -y sudo \
    && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
    && chmod 0440 /etc/sudoers.d/$USERNAME

# Add picoprobe hardware to 

RUN echo "# Raspberry Pi Picoprobe\nATTRS{idVendor}==\"2e8a\", ATTRS{idProduct}==\"0004\", MODE:=\"0666\"" 
    # >> /etc/udev/rules.d/99-openocd.rules && \
    # udevadm trigger

#Set the default user
USER $USERNAME

RUN curl https://sh.rustup.rs -sSf | bash -s -- -y \
    && echo 'source $HOME/.cargo/env' >> $HOME/.bashrc \
    && source $HOME/.cargo/env \
    && rustup self update \
    && rustup update stable \
    && rustup target add thumbv6m-none-eabi \
    && cargo install elf2uf2-rs \
    && cargo install probe-run

ENV PATH="$HOME/.cargo/bin:${PATH}"

COPY .cargo/config /workspaces/.cargo/config

CMD ["sleep","infinity"]