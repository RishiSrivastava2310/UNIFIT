# UNIFIT

Retail / E-Commerce Management & Commerce Platform

## Requirements

- Java Development Kit (JDK) 25. The Maven project currently sets `java.version` to 25; use `java -version` to check your active JDK. Do not change this version independently.
- MySQL Server 8 or later for local application development. The MySQL driver is included, but database connection settings are not committed. The health endpoint and automated tests do not require a running MySQL server.
- Git. Maven is included through the Maven Wrapper, so a separate Maven installation is not required.

## Run the tests

From the `UNIFIT/` project directory:

```bash
./mvnw test
```

On Windows, use `mvnw.cmd test` from the same directory. Tests use an in-memory H2 database and do not use local MySQL credentials.

## Run locally with MySQL

1. Install and start MySQL Server 8.4 or later.
2. Create a local database and a database user for UNIFIT.
3. In `UNIFIT/src/main/resources/`, create `application-local.properties` with your local connection details:

   ```properties
   spring.datasource.url=jdbc:mysql://localhost:3306/unifit
   spring.datasource.username=YOUR_LOCAL_USERNAME
   spring.datasource.password=YOUR_LOCAL_PASSWORD
   spring.jpa.hibernate.ddl-auto=update
   ```

   Replace the example username and password locally. Never commit this file or put real credentials in shared files.
4. From the `UNIFIT/` project directory, start the app with the local profile:

   ```bash
   ./mvnw spring-boot:run -Dspring-boot.run.profiles=local
   ```

   On Windows, use `mvnw.cmd spring-boot:run -Dspring-boot.run.profiles=local`.
5. Open `http://localhost:8080/`; the current health endpoint responds with `UNIFIT backend is running!`.

The `application-local.properties` file is ignored by Git. Keep database passwords there, not in `application.properties`, source code, or commits.

## Git workflow

Before starting work, update your local `main` branch:

```bash
git switch main
git pull origin main
```

For shared work, create a feature branch from the updated `main`. Review `git status` and the exact staged files before committing. Push the feature branch and open a pull request so both collaborators can review changes before they reach `main`.

```bash
git add path/to/file
git diff --cached
git commit -m "Describe your changes"
git push -u origin your-branch-name
```

Do not add local configuration, passwords, `.idea/`, or `target/` to Git. Avoid pushing directly to `main` when the other collaborator may also be changing it.

## Git Workflow

### Before Starting Work

Pull the latest changes from GitHub before making any changes locally.

```bash
git pull origin main
```

### After Finishing Work

Save and push your changes to GitHub.

```bash
git add .
git commit -m "Describe your changes"
git push origin main
```

### Quick Reference

- **Before work:** `git pull origin main`
- **After work:** `git add .` → `git commit -m "message"` → `git push origin main`
- Always write a meaningful commit message describing your changes.
- Check `git status` before committing to review modified files.
