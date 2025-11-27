ARG BUILD_FROM
FROM $BUILD_FROM

# Install Rust and build dependencies
RUN apk add --no-cache \
    cargo \
    rust \
    openssl-dev \
    musl-dev

# Copy source code
WORKDIR /build
COPY . .

# Build the project
RUN cargo build --release

# Copy built binary and assets
RUN mkdir -p /app && \
    cp target/release/govee /app/ && \
    cp -r assets /app/assets/ && \
    cp AmazonRootCA1.pem /app/

# Setup runtime
COPY run.sh /run.sh
RUN chmod +x /run.sh

CMD [ "/run.sh" ]