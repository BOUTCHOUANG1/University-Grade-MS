# University Grade Management System
University Grade Management System (University-GMS) is a Spring Boot 3.5.6 application built with Java 21, Maven, PostgreSQL, and includes JPA, Spring Security, JWT authentication, email functionality, and Flyway database migrations.

Always reference these instructions first and fallback to search or bash commands only when you encounter unexpected information that does not match the info here.

## Working Effectively

### Java Setup (CRITICAL)
- Install Java 21 (required - Spring Boot 3.5.6 requires Java 21):
  - `sudo apt update && sudo apt install -y openjdk-21-jdk`
  - `sudo update-alternatives --config java` and select Java 21 option (usually option 1)
  - `export JAVA_HOME=/usr/lib/jvm/java-21-openjdk-amd64`
  - Verify: `java -version` should show "21.0.8" or higher

### Build and Test the Repository:
- Initial compile: `./mvnw compile` -- takes 3 seconds after dependencies are cached. NEVER CANCEL. Set timeout to 60+ seconds for first run (downloads dependencies).
- Clean compile: `./mvnw clean compile` -- takes 25 seconds. NEVER CANCEL. Set timeout to 60+ seconds.
- Full build (without tests): `./mvnw clean package -DskipTests` -- takes 10 seconds. NEVER CANCEL. Set timeout to 60+ seconds.
- Full build (with tests - WILL FAIL): `./mvnw clean package` -- takes 10 seconds and fails due to missing database configuration. Tests require database setup.

### Running the Application:
- ALWAYS set `export JAVA_HOME=/usr/lib/jvm/java-21-openjdk-amd64` before running any Java/Maven commands.
- Run with Maven plugin: `./mvnw spring-boot:run` -- starts in 3 seconds but fails without database configuration.
- Run JAR directly: `java -jar target/university_GMS-0.0.1-SNAPSHOT.jar` -- starts in 2 seconds but fails without database configuration.
- Application runs on port 8080 by default (http://localhost:8080).

### Database Requirements (CRITICAL):
- Application requires PostgreSQL database configuration to start successfully.
- Without database configuration, application fails with: "Failed to configure a DataSource: 'url' attribute is not specified"
- Tests require database connection or H2 dependency (not currently included).
- Application uses Flyway for database migrations.

## Validation

### Build Validation:
- Always run `./mvnw clean compile` to verify code compiles correctly.
- Always run `./mvnw clean package -DskipTests` to build the executable JAR.
- Build artifacts are created in `target/` directory:
  - `target/university_GMS-0.0.1-SNAPSHOT.jar` (executable Spring Boot JAR - 66MB)
  - `target/university_GMS-0.0.1-SNAPSHOT.jar.original` (original JAR - 3KB)

### Application Validation:
- Verify application starts with: `timeout 30s ./mvnw spring-boot:run`
- Application will fail without database but should show Spring Boot banner and proper error message about DataSource configuration.
- Successful startup shows: Tomcat initialized with port 8080, Spring Data JPA repositories scanning.

### Test Validation:
- Tests currently CANNOT run without database configuration.
- Running `./mvnw test` fails with database connection errors.
- Skipping tests: `./mvnw test -DskipTests` or include `-DskipTests` in package command.

## Timing Expectations (NEVER CANCEL)
- **Initial dependency download**: 25+ seconds. NEVER CANCEL. Set timeout to 120+ seconds.
- **Clean compile**: 25 seconds. NEVER CANCEL. Set timeout to 60+ seconds.
- **Incremental compile**: 3 seconds. Set timeout to 30+ seconds.
- **Package build**: 10 seconds. NEVER CANCEL. Set timeout to 60+ seconds.
- **Application startup**: 3 seconds to failure point (without database). Set timeout to 60+ seconds.

## Common Tasks

### Development Workflow:
1. Make code changes
2. Compile: `./mvnw compile`
3. Test build: `./mvnw package -DskipTests`
4. Verify startup: `timeout 30s ./mvnw spring-boot:run`

### Working with Tests:
- Tests currently require database setup to run successfully.
- Skip tests during development: `./mvnw clean package -DskipTests`
- To enable tests, add H2 dependency to pom.xml or configure PostgreSQL database.

### Working with the Application:
- Application architecture: Spring Boot web application with embedded Tomcat
- Main class: `com.nathan.university_gms.UniversityGmsApplication`
- Configuration: `src/main/resources/application.properties` (minimal - only sets application name)
- Dependencies include: Spring Security, JPA, JWT, ModelMapper, Flyway, Email support

## Frequently Referenced Information

### Repository Structure:
```
.
├── .github/                    # GitHub templates and configurations
│   ├── ISSUE_TEMPLATE/        # Bug report, feature request, chore templates
│   ├── README.md              # GitHub workflow documentation
│   ├── REPOSITORY_CONFIGURATION.md  # Branch protection, labels setup
│   └── pull_request_template.md
├── .mvn/wrapper/              # Maven wrapper files
├── src/
│   ├── main/java/com/nathan/university_gms/
│   │   └── UniversityGmsApplication.java  # Main Spring Boot application class
│   ├── main/resources/
│   │   └── application.properties          # Application configuration
│   └── test/java/com/nathan/university_gms/
│       └── UniversityGmsApplicationTests.java  # Basic context test
├── target/                    # Build output directory
├── mvnw                      # Maven wrapper script (executable)
├── mvnw.cmd                  # Maven wrapper for Windows
└── pom.xml                   # Maven project configuration
```

### Key Commands Quick Reference:
```bash
# Setup Java 21 (required)
export JAVA_HOME=/usr/lib/jvm/java-21-openjdk-amd64

# Build commands
./mvnw clean                           # Clean build artifacts
./mvnw compile                         # Compile source code
./mvnw clean compile                   # Clean and compile
./mvnw clean package -DskipTests       # Build executable JAR
./mvnw clean package                   # Build with tests (fails without DB)

# Run commands
./mvnw spring-boot:run                 # Run with Maven plugin
java -jar target/university_GMS-0.0.1-SNAPSHOT.jar  # Run JAR directly

# Help commands
./mvnw help:describe -Dplugin=org.springframework.boot:spring-boot-maven-plugin
./mvnw --version                       # Show Maven and Java versions
```

### Dependencies Overview:
- Spring Boot Starter: Web, JPA, Security, Validation, Mail, DevTools
- Database: PostgreSQL runtime, Flyway migrations
- Security: Spring Security, JWT (jjwt 0.12.5)
- Utilities: ModelMapper 3.2.4
- Testing: Spring Boot Test, Spring Security Test

### Development Notes:
- Java 21 requirement is strict - application will not compile with older Java versions.
- Database configuration is required for application startup and tests.
- Maven wrapper (`./mvnw`) is preferred over global Maven installation.
- Application includes Spring Boot DevTools for development hot-reloading.
- Security is enabled by default - endpoints may require authentication.

## Troubleshooting

### Common Issues:
1. **Java version mismatch**: Ensure Java 21 is installed and `JAVA_HOME` is set correctly.
2. **Database connection failure**: Expected behavior without database configuration.
3. **Build timeouts**: Increase timeout values, especially for first-time dependency downloads.
4. **Test failures**: Tests require database configuration - use `-DskipTests` to skip.

### Error Messages to Expect:
- "Failed to configure a DataSource" - Normal without database setup
- "Failed to load driver class" - Normal without H2 or PostgreSQL configuration
- Java version errors - Upgrade to Java 21

Always verify your changes work by running the build and startup validation steps above.