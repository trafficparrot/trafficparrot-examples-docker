# Traffic Parrot Docker Examples

This repository contains example Dockerfiles for running Traffic Parrot in Docker containers.

For more information, see the [Traffic Parrot Docker documentation](https://trafficparrot.com/documentation/?redirectToLatest=true&path=/user_guide.html#running-docker)

## Available Examples

- [docker-java-17-temurin](docker-java-17-temurin) - Traffic Parrot with Eclipse Temurin OpenJDK 17 LTS
- [docker-java-17-alpine](docker-java-17-alpine) - Traffic Parrot with Alpine Linux and OpenJDK 17
- [docker-java-21-temurin](docker-java-21-temurin) - Traffic Parrot with Eclipse Temurin OpenJDK 21 LTS
- [docker-java-21-alpine](docker-java-21-alpine) - Traffic Parrot with Alpine Linux and OpenJDK 21 LTS

## Docker Usage Guidelines

### Recommended Docker Setup
- Use OpenJDK JRE images (Java 17 or newer)
- Ensure the container has:
  * bash
  * java (if using the no-jre bundle)
  * glibc library

### Best Practices
- Prefer bundled JRE distribution per OS instead of no-JRE bundle
- Expose necessary ports from `trafficparrot.properties`
- Use start-foreground.sh to ensure proper process management
- Stop containers gracefully using "docker stop" to release license seats

### DO and DO NOT
- **DO** use `docker stop` to gracefully stop containers which properly releases license seats
- **DO NOT** use `docker kill` as it prevents proper termination

## Building and Running

To build an image:
```bash
docker build -t trafficparrot .
```

### Building Linux Images on macOS

When building Linux-based Docker images on macOS, you need to specify the platform using the `--platform` flag:

```bash
docker build --platform linux/amd64 -t trafficparrot .
```

For ARM-based Macs (M1/M2/M3), you may also use:

```bash
docker build --platform linux/arm64 -t trafficparrot .
```

Note that the appropriate platform depends on where you plan to run the container. For maximum compatibility, build with `linux/amd64`.

### Running the Container

To run a container:
```bash
docker run --name trafficparrot -d -p 127.0.0.1:8080:8080 [other ports as needed] trafficparrot
```

Wait for Traffic Parrot to start up, then access the web UI at http://127.0.0.1:8080

## Configuration with Environment Variables

You can pass configuration via environment variables:

```bash
docker run -p 18080:18080 -e GUI_HTTP_PORT=18080 trafficparrot
```

And modify the `CMD` in the `Dockerfile` to use these variables:

```dockerfile
ENV GUI_HTTP_PORT=8080
CMD exec ./start-foreground.sh trafficparrot.gui.http.port=$GUI_HTTP_PORT
```

## Logging Configuration

Logging levels can be set dynamically via environment variables with support for log4j, log4j2, and logback configurations:

```dockerfile
# Set logging level via environment variable
ENV LOG_LEVEL=ERROR

# Configure start command to use the environment variable
CMD exec ./start-foreground.sh -DLOG_LEVEL=$LOG_LEVEL
```

Depending on your logging configuration file:

- For **log4j.properties**:
  ```
  log4j.rootLogger=${LOG_LEVEL},file,stdout
  ```

- For **log4j2.xml**:
  ```xml
  <Root level="${env:LOG_LEVEL}">
  ```

- For **logback.xml**:
  ```xml
  <root level="${LOG_LEVEL}">
  ```

When running the container, specify the logging level:
```bash
docker run -p 8080:8080 -e LOG_LEVEL=DEBUG trafficparrot
```

## License

See the [LICENSE](LICENSE) file for license details.