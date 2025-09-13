# Stage 1: dummy backend
FROM openjdk:17-jdk-alpine AS backend-build

# Create dummy app
WORKDIR /app
RUN echo 'public class Main { public static void main(String[] args) { System.out.println("Hello PolyCloud!"); } }' > Main.java
RUN javac Main.java

# Stage 2: dummy frontend
FROM node:18-alpine AS frontend-build
WORKDIR /app
RUN mkdir -p src
RUN echo 'console.log("Dummy frontend built");' > src/index.js

# Stage 3: final image
FROM alpine:latest
WORKDIR /app
COPY --from=backend-build /app/Main.class .
COPY --from=frontend-build /app/src /app/frontend
CMD ["echo", "PolyCloud dummy image ready!"]
