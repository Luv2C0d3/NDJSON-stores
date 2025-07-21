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

# Verify installs (optional)
#RUN swift --version && go version && elixir --version && node --version && python3 --version && rustc --version && clojure --version

