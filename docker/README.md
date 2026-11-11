# Docker -- Product DevOps Project

## Overview

This directory contains Dockerfiles and Docker Compose configuration
used to containerize and run multiple microservices as part of the
Product DevOps Project.

The project demonstrates practical Docker concepts, including:

-   Dockerfile creation
-   Multi-stage Docker builds
-   Docker image creation
-   Containerization of microservices
-   Docker Compose
-   Environment variable management
-   Port mapping
-   Resource limits and reservations
-   Service dependencies
-   Container restart policies

## Project Structure

docker/
|---> Golang.Dockerfile
|---> python.Dockerfile
|---> docker-compose.yml
|---> .env
|---> README.md

## Dockerfiles

### 1. Golang.Dockerfile -- Product Catalog Service

-   Base image: "golang:1.22-alpine"
-   Uses a multi-stage build.
-   The builder stage compiles the Go application.
-   The Alpine runtime stage runs the compiled application.
-   Service port: "8088"

### 2. gradle.Dockerfile -- Ad Service

-   Uses Java 21 JDK for the build stage.
-   Uses Java 21 JRE for the runtime stage.
-   Implements a multi-stage Docker build.
-   Service port: "9555"

### 3. python.Dockerfile -- Recommendation Service

-   Base image: "python:3.12-slim-bookworm"
-   Used to containerize the Python application.
-   Service port: "1010"

## Docker Compose

The "docker-compose.yml" file defines and manages the following
services:

  Service                       Port
  ------------------------- --------
  "adservice"                 "9555"
  "product-catalog"           "8088"
  "recommendationservice"     "1010"

### Compose Configuration Features

-   Multiple service management
-   Port mapping
-   Environment variable configuration
-   CPU and memory limits
-   Resource reservations
-   Restart policies
-   Service dependencies

The Recommendation Service depends on the Product Catalog Service.

## Environment Variables

The ".env" file stores configuration values used by Docker Compose.

It may include:

-   Docker image names
-   Service ports
-   OpenTelemetry service names
-   CPU limits and reservations
-   Memory limits and reservations

Environment variables keep configuration separate from the Compose file.
Do not commit secrets or credentials to a public repository.

## Build Docker Images

The Compose configuration uses "image:" rather than "build:", so build
the images independently before starting the services.

Run the following commands from the directory and context expected by
each Dockerfile. Replace each placeholder with the correct application
build context:


docker build -f Golang.Dockerfile -t product-catalog:latest <product-catalog-context>

docker build -f gradle.Dockerfile -t adservice:latest <adservice-context>

docker build -f python.Dockerfile -t recommendationservice:latest <recommendation-context>


Make sure the image tags match the image names configured in ".env". If
your Dockerfiles are in a separate directory from the application
source, adjust the Dockerfile paths and build contexts accordingly.

## Start Services

After building all required images and checking the ".env"
configuration:

docker compose up -d

## Verify Running Containers

docker ps

## View Container Logs

View logs for all services:

docker compose logs

View logs for an individual service:

docker compose logs adservice
docker compose logs product-catalog
docker compose logs recommendationservice

## Stop Services

docker compose down

## Learning Outcomes

Through this hands-on implementation, the following concepts are
practiced:

1.  Writing Dockerfiles for applications built with different
    technologies.
2.  Understanding multi-stage Docker builds.
3.  Building Docker images independently.
4.  Running multiple microservices using Docker Compose.
5.  Managing environment variables using ".env".
6.  Configuring service ports and dependencies.
7.  Applying container resource constraints.
8.  Monitoring and managing running containers.

## Important Verification Notes

Before treating this README as a record of the final working setup,
verify these details against the actual files:

-   Confirm that the image names and tags in ".env" match the tags used
    in the "docker build" commands.
-   Confirm the Docker build contexts and paths for all three
    Dockerfiles.
-   Check that the Compose service names match the names used in the log
    commands.
-   If a Dockerfile uses a build argument such as
    "${PRODUCT_CATALOG_PORT}", confirm that the argument is declared and
    passed correctly.
-   Confirm that the ports and service dependency described above match
    the current "docker-compose.yml".

------------------------------------------------------------------------

**Project:** Product DevOps Project\
**Section:** Docker\
**Purpose:** Hands-on Docker learning and microservices
containerization.
