# Java/Spring Dev Container Template

This repository provides a lean dev container template for Java and Spring Boot projects.

It includes:

- a dev container based on Liberica OpenJDK 25
- a practical set of VS Code extensions for Java, Spring, YAML, and REST requests
- a persistent Maven cache backed by a Docker volume
- a lightweight container setup without a globally installed Maven

## Requirements

- VS Code
- the `Dev Containers` extension
- a running Docker-compatible engine such as Docker Desktop or OrbStack

## Usage

There are two intended ways to use this setup.

### 1. Copy `.devcontainer` into an existing Java/Spring project

Copy the `.devcontainer` folder from this repository into the root directory of your existing project.

Example:

```text
my-spring-project/
  .devcontainer/
    devcontainer.json
    Dockerfile
  mvnw
  pom.xml
  src/
```

After that:

1. Open the project folder in VS Code.
2. If needed, reload or restart VS Code.
3. Confirm the `Reopen in Container` prompt or run `Dev Containers: Reopen in Container`.
4. VS Code builds the image and starts the development container.

During the first start, the `postCreateCommand` is executed. If an `mvnw` file exists, it is made executable and verified.

### 2. Use this repository as a template

If you want to start new projects with the same baseline setup, you can use this repository as a template repository.

Typical flow:

1. Select `Use this template` on GitHub.
2. Create a new repository from this template.
3. Add your project code to the new repository.
4. Open the generated repository in VS Code.
5. Start the container via `Reopen in Container`.

This is useful if you want the same starting point for every new Java/Spring project.

## What happens on startup

When you open the project folder in VS Code and start the dev container, the following happens:

1. VS Code detects `.devcontainer/devcontainer.json`.
2. The image is built from `.devcontainer/Dockerfile`.
3. The project folder is mounted into the container under `/workspaces/<project-name>`.
4. The Docker volume `maven-cache` is mounted to `/home/vscode/.m2`.
5. The configured extensions are installed inside the container.
6. The VS Code settings from `devcontainer.json` are applied for the container session.

## Notes

- Maven is not installed globally inside the container. Projects are expected to use the Maven Wrapper (`mvnw`).
- After changing `Dockerfile` or `devcontainer.json`, run `Dev Containers: Rebuild Container`.
- The `maven-cache` volume is created only when the container is built or started for the first time.

## Files

- `.devcontainer/devcontainer.json`: VS Code and container configuration
- `.devcontainer/Dockerfile`: base image and required tools inside the container