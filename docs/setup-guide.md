# Setup Guide: Java and Maven

This guide explains how to build and run JPetStore (jpetstore-6-sme) on your own computer.

## 1. Prerequisites

| Tool | Version | How to check |
|---|---|---|
| JDK | 8 (Java 1.8) | `java -version` |
| Maven | Not required to install; the project includes the Maven Wrapper (`mvnw`) | `./mvnw -v` |
| Git | Any recent version | `git --version` |
| Docker (optional) | Only for the Docker method in section 5 | `docker --version` |

## 2. Get the source code

```bash
git clone https://github.com/<leader-username>/jpetstore-6-sme.git
cd jpetstore-6-sme
```

## 3. Build the project

macOS / Linux:
```bash
./mvnw clean package
```

Windows:
```cmd
mvnw.cmd clean package
```

When the build succeeds, the WAR file is created in the `target/` folder.

## 4. Run the application

macOS / Linux:
```bash
./mvnw cargo:run -P tomcat90
```

Windows:
```cmd
mvnw.cmd cargo:run -P tomcat90
```

Wait until the console shows that the server has started, then open:

**http://localhost:8080/jpetstore/**

Press `Ctrl + C` in the terminal to stop the server.

## 5. Alternative: run with Docker

```bash
docker build . -t jpetstore
docker run -p 8080:8080 jpetstore
```

Or with Docker Compose:
```bash
docker compose up -d
```

## 6. Run the integration tests (optional)

```bash
./mvnw clean verify -P tomcat90
```

## 7. Quick check that it works

1. Open http://localhost:8080/jpetstore/ in a browser.
2. The JPetStore home page should appear.
3. Click a pet category (for example Fish) to confirm the catalog loads.

## 8. Common problems

For installation errors and fixes, see `docs/troubleshooting.md`.