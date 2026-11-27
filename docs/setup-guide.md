# Setup Guide: Java and Maven

This guide explains how to build and run JPetStore (jpetstore-6-sme) on your own computer.

## 1. Prerequisites

| Tool | Version | How to check |
|---|---|---|
| JDK | **21** | `java -version` |
| Maven | Not required to install; the Maven Wrapper (`mvnw`) is included in the repo | `./mvnw -version` |
| Git | Any recent version | `git --version` |
| VS Code | Any recent version (optional, for editing) | |
| Docker | Optional, only for Method B | `docker --version` |

> **Note:** The project is compiled to Java 8 bytecode (so Java 8 appears in `pom.xml`), but
> you should run the build with **JDK 21**. If your computer has a different JDK (for example 25),
> switch to JDK 21 first (see section 6).

## 2. Get the source code

```bash
git clone https://github.com/bob3528/jpetstore-6-sme.git
cd jpetstore-6-sme
code .
```

## 3. Method A: Maven and Tomcat (recommended)

**Step 1: Verify Java and Maven**

macOS / Linux:
```bash
java -version
./mvnw -version
```

Windows:
```cmd
java -version
mvnw.cmd -version
```

Make sure it shows Java 21.

**Step 2: Build the project**

macOS / Linux:
```bash
./mvnw clean package
```

Windows:
```cmd
mvnw.cmd clean package
```

Wait until the terminal shows `BUILD SUCCESS` (the first build takes a few minutes while
dependencies download). All 98 unit tests should pass.

**Step 3: Run the application**

macOS / Linux:
```bash
./mvnw cargo:run -P tomcat9
```

Windows:
```cmd
mvnw.cmd cargo:run -P tomcat9
```

Wait for the message `Tomcat 9.0.120 started on port [8080]`.

**Step 4: Open the application**

Go to **http://localhost:8080/jpetstore/** in your browser.

**Step 5: Stop the server**

Press `Ctrl + C` in the terminal.

## 4. Method B: Docker (alternative)

Requires Docker Desktop to be running.

```bash
docker compose up -d --build
```

Then open http://localhost:8080/jpetstore/. Stop it with `docker compose down`.

> **Known issue:** If the build fails with `openjdk:25: not found`, change line 17 of the
> `Dockerfile` to `FROM eclipse-temurin:21-jdk`.

## 5. Quick check that it works

1. Open http://localhost:8080/jpetstore/.
2. The JPetStore home page should appear.
3. Click a pet category (for example Fish) to confirm the catalog loads.

## 6. Switching JDK versions

macOS:
```bash
/usr/libexec/java_home -V
export JAVA_HOME=$(/usr/libexec/java_home -v 21)
java -version
```

Windows (Command Prompt):
```cmd
set JAVA_HOME=C:\Program Files\Java\jdk-21
set PATH=%JAVA_HOME%\bin;%PATH%
java -version
```

This only applies to the terminal window where you ran it.

## 7. Harmless warnings during the build

These can be ignored, because the build still ends with `BUILD SUCCESS`:
- `source value 8 is obsolete`: the project targets Java 8 bytecode.
- `There were problems parsing ... .jsp` and `XmlParsingException`: a code-cleanup plugin
  cannot read JSP files as XML.

## 8. Other problems

For installation errors and fixes, see `docs/troubleshooting.md`.