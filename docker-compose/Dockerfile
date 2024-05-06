FROM docker.io/bitnami/keycloak:24.0.2-debian-12-r0

# Copy your custom SPI JAR file
COPY ./requiredaction.jar /opt/bitnami/keycloak/providers/

# Enable debug mode
ENV DEBUG=true

# Run build command
RUN /opt/bitnami/keycloak/bin/kc.sh build