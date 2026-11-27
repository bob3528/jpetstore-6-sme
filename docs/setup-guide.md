# Setup Guide: Java and Maven

How to build and run JPetStore (jpetstore-6-sme) on your computer.

## 1. What you need

- **JDK 21** (check with `java -version`)
- **Git**
- **VS Code** (optional, for editing)

Maven doesn't need installing, because the project includes the Maven Wrapper (`mvnw`).

> The project is compiled to Java 8 bytecode, so Java 8 appears in `pom.xml`. You should still run it with JDK 21.

## 2. Get the code

```bash
git clone https://github.com/bob3528/jpetstore-6-sme.git
cd jpetstore-6-sme
code .
```

## 3. Check Java and Maven

```bash
java -version
./mvnw -version
```

It should show Java 21. On Windows, use `mvnw.cmd` instead of `./mvnw` in every command in this guide.

## 4. Build

```bash
./mvnw clean package
```

Wait for `BUILD SUCCESS`. The first build takes a few minutes because it downloads dependencies. All 98 tests should pass.

## 5. Run

```bash
./mvnw cargo:run -P tomcat9
```

Wait for `Tomcat 9.0.120 started on port [8080]`, then open:

**http://localhost:8080/jpetstore/**

## 6. Stop and restart

**To stop:** press `Ctrl + C` in the terminal.

**To start again:** run the same command from the project folder:

```bash
./mvnw cargo:run -P tomcat9
```

You don't need to build again unless the code has changed. If you edited the code, run `./mvnw clean package` first, then the run command.

If it says port 8080 is already in use, the old server is still running. Find that terminal and press `Ctrl + C`, or close it.

## 7. Wrong JDK version?

If `java -version` doesn't show 21:

macOS:
```bash
export JAVA_HOME=$(/usr/libexec/java_home -v 21)
java -version
```

Windows (Command Prompt):
```cmd
set JAVA_HOME=C:\Program Files\Java\jdk-21
set PATH=%JAVA_HOME%\bin;%PATH%
java -version
```

This only applies to the terminal window where you typed it.

## 8. Warnings you can ignore

The build still ends with `BUILD SUCCESS` despite these:
- `source value 8 is obsolete`
- `There were problems parsing ... .jsp` and `XmlParsingException` (a code-cleanup plugin can't read JSP files)

## 9. Other problems

See `docs/troubleshooting.md`.