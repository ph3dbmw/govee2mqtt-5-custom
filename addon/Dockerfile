ARG BUILD_FROM
FROM $BUILD_FROM

# Copy pre-built binary and assets
COPY bin/govee /app/govee
COPY ../assets /app/assets/
COPY ../AmazonRootCA1.pem /app/

# Setup runtime
COPY run.sh /run.sh
RUN chmod +x /run.sh /app/govee

CMD [ "/run.sh" ]