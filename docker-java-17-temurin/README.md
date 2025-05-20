# Traffic Parrot with Eclipse Temurin OpenJDK 17

This example uses the Eclipse Temurin OpenJDK 17 JRE as the base image for running Traffic Parrot.

## Base Image

```
eclipse-temurin:17-jre
```

## Features

- Uses official Eclipse Temurin OpenJDK 17 JRE image
- Includes unzip for extracting the Traffic Parrot distribution
- Sets appropriate permissions for running in containerized environments
- Uses start-foreground.sh script for proper process management

## Building the Image

```bash
# Copy your Traffic Parrot zip to this directory
cd docker-java-17-temurin
cp /path/to/your/trafficparrot-*.zip .

# Build the image
docker build -t trafficparrot:17-temurin .

# If building on macOS for Linux environments
docker build --platform linux/amd64 -t trafficparrot:17-temurin .
```

## Running the Container

```bash
docker run -p 8080:8080 -p 8081:8081 trafficparrot:17-temurin
```

## Important Notes

- This example uses Java 17, the minimum required version for Traffic Parrot 5.53+
- Remember to expose all required ports based on your Traffic Parrot configuration
- Always use `docker stop` to properly shut down Traffic Parrot and release license seats