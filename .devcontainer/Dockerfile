# Gunakan image Debian Stable sebagai base image
FROM debian:stable

# Set environment variable TERM untuk mendukung warna terminal
ENV TERM=xterm-256color

# Update dan install dependensi yang dibutuhkan
RUN apt update && apt upgrade -y && \
    apt install -y \
    neofetch \
    xauth \
    ninja-build \
    gettext \
    cmake \
    unzip \
    curl \
    build-essential \
    qemu-system \
    git

# Clone dan install Neovim dari repositori GitHub
WORKDIR /neovim
RUN git clone https://github.com/neovim/neovim /neovim
RUN git checkout stable
RUN make CMAKE_BUILD_TYPE=RelWithDebInfo
RUN make install
RUN cd .. && rm -rf neovim

# Clone konfigurasi NvChad untuk Neovim
RUN git clone https://github.com/izzalDev/NvChad.git ~/.config/nvim

# Install plugin menggunakan Lazy neovim secara headless
RUN nvim --headless "+Lazy! sync" +qa

# Expose port untuk pengembangan (port 9000)
EXPOSE 9000

# Gunakan bash sebagai entrypoint default
WORKDIR /
CMD ["/bin/bash"]
