FROM swift:6.1.2

ENV DEBIAN_FRONTEND=noninteractive

# Install basic tools + Go, Elixir, NodeJS, Python, Rust, Clojure dependencies
RUN apt-get update && apt-get install -y --no-install-recommends \
    curl git build-essential \
    golang-go \
    elixir \
    nodejs npm \
    python3 python3-pip python3-venv \
    default-jre-headless openjdk-17-jdk-headless \
    unzip wget \
 && apt-get clean && rm -rf /var/lib/apt/lists/*

# Install Rust using official rustup script
RUN curl https://sh.rustup.rs -sSf | sh -s -- -y
ENV PATH="/root/.cargo/bin:${PATH}"

# Install Clojure CLI tools
RUN curl -L -O https://github.com/clojure/brew-install/releases/latest/download/linux-install.sh && \
    chmod +x linux-install.sh && \
    ./linux-install.sh && \
    rm linux-install.sh

RUN apt-get update && apt-get install -y bash-completion

ARG USER_UID=1000
ARG USER_GID=1000
ARG USERNAME=devuser

RUN groupadd --gid $USER_GID $USERNAME && \
    useradd --uid $USER_UID --gid $USER_GID -s /bin/bash --create-home $USERNAME

# Copy a basic .bashrc to user's home
COPY bashrc /home/$USERNAME/.bashrc
RUN chown $USERNAME:$USERNAME /home/$USERNAME/.bashrc
    
USER $USERNAME
WORKDIR /home/$USERNAME

# Install any dependencies, e.g. Elixir Hex
RUN mix local.hex --force && mix local.rebar --force


# Verify installs (optional)
#RUN swift --version && go version && elixir --version && node --version && python3 --version && rustc --version && clojure --version

CMD ["bash"]