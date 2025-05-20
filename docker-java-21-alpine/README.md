# Traffic Parrot with Alpine Linux and OpenJDK 21 LTS

This example uses Alpine Linux with OpenJDK 21 LTS JRE for running Traffic Parrot in a lightweight container.

## Base Image

```
alpine:3
```

## Features

- Lightweight Alpine Linux base (significantly smaller image size)
- Adds OpenJDK 21 LTS JRE, bash, and required compatibility libraries
- Sets appropriate permissions for running in containerized environments
- Configures `LD_LIBRARY_PATH` for proper library resolution
- Uses start-foreground.sh script for proper process management

## Building the Image

```bash
# Copy your Traffic Parrot zip to this directory
cd docker-java-21-alpine
cp /path/to/your/trafficparrot-*.zip .

# Build the image
docker build -t trafficparrot:21-alpine .

# If building on macOS for Linux environments
docker build --platform linux/amd64 -t trafficparrot:21-alpine .
```

## Running the Container

```bash
docker run -p 8080:8080 -p 8081:8081 trafficparrot:21-alpine
```

## Important Notes

- The image includes `libc6-compat` and `gcompat` for compatibility with glibc-based applications
- The `LD_LIBRARY_PATH` environment variable is set to ensure proper library resolution
- This example uses Java 21, the latest LTS version
- Remember to expose all required ports based on your Traffic Parrot configuration
- Always use `docker stop` to properly shut down Traffic Parrot and release license seats
