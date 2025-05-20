# Traffic Parrot with Eclipse Temurin OpenJDK 21 LTS

This example uses the Eclipse Temurin OpenJDK 21 LTS JRE as the base image for running Traffic Parrot.

## Base Image

```
eclipse-temurin:21-jre
```

## Features

- Uses official Eclipse Temurin OpenJDK 21 LTS JRE image (latest LTS version)
- Includes unzip for extracting the Traffic Parrot distribution
- Sets appropriate permissions for running in containerized environments
- Uses start-foreground.sh script for proper process management

## Building the Image

```bash
# Copy your Traffic Parrot zip to this directory
cd docker-java-21-temurin
cp /path/to/your/trafficparrot-*.zip .

# Build the image
docker build -t trafficparrot:21-temurin .

# If building on macOS for Linux environments
docker build --platform linux/amd64 -t trafficparrot:21-temurin .
```

## Running the Container

```bash
docker run -p 8080:8080 -p 8081:8081 trafficparrot:21-temurin
```

## Important Notes

- This example uses Java 21
- Remember to expose all required ports based on your Traffic Parrot configuration
- Always use `docker stop` to properly shut down Traffic Parrot and release license seats