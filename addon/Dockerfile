ARG BUILD_FROM
FROM $BUILD_FROM

# Install Rust and build dependencies
RUN apt-get update && apt-get install -y \
    curl \
    build-essential \
    libssl-dev \
    pkg-config \
    && rm -rf /var/lib/apt/lists/*

# Install Rust
RUN curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y
ENV PATH="/root/.cargo/bin:${PATH}"

# Copy source code
WORKDIR /build
COPY . .

# Build the project
RUN cargo build --release

# Copy built binary and assets to /app
RUN mkdir -p /app && \
    cp target/release/govee /app/ && \
    cp -r assets /app/assets/ && \
    cp AmazonRootCA1.pem /app/

# Setup runtime
WORKDIR /
COPY run.sh /run.sh
RUN chmod +x /run.sh

CMD [ "/run.sh" ]