# University Grade Management System

The University Grade Management System is a Spring Boot web application for managing university grades. It features JWT authentication, PostgreSQL database integration, Flyway migrations, email notifications, and secure grade management functionality.

Always reference these instructions first and fallback to search or bash commands only when you encounter unexpected information that does not match the info here.

## Working Effectively

### Prerequisites and Environment Setup
- Install Java 21 JDK (NOT Java 17 or earlier versions):
  ```bash
  sudo apt update && sudo apt install -y openjdk-21-jdk
  export JAVA_HOME=/usr/lib/jvm/java-21-openjdk-amd64
  export PATH=$JAVA_HOME/bin:$PATH
  ```
- Verify Java version: `java --version` (must show version 21.x.x)
- Maven is included via Maven Wrapper (./mvnw), no separate installation needed

### Build and Test Commands
- **Bootstrap and build** the repository:
  ```bash
  cd /path/to/University-Grade-MS
  export JAVA_HOME=/usr/lib/jvm/java-21-openjdk-amd64
  export PATH=$JAVA_HOME/bin:$PATH
  ./mvnw clean compile
  ```
  - Takes ~3-5 seconds. NEVER CANCEL. Set timeout to 60+ seconds for safety.

- **Full build with packaging**:
  ```bash
  ./mvnw clean package -DskipTests
  ```
  - Takes ~8-10 seconds. NEVER CANCEL. Set timeout to 60+ seconds.

- **Run tests** (requires database configuration):
  ```bash
  ./mvnw test
  ```
  - Takes ~5-6 seconds with proper database setup. NEVER CANCEL. Set timeout to 60+ seconds.
  - **IMPORTANT**: Tests will FAIL without database configuration. See Database Setup section.

### Database Setup

#### Production Database
- Uses PostgreSQL database
- Configure via `application.properties` or environment variables
- Production configuration not included in repository

#### Development/Testing Database
For development and testing, add H2 in-memory database:

1. **Add H2 dependency to pom.xml**:
   ```xml
   <dependency>
       <groupId>com.h2database</groupId>
       <artifactId>h2</artifactId>
       <scope>runtime</scope>
   </dependency>
   ```

2. **Create `src/main/resources/application-dev.properties`**:
   ```properties
   # Development configuration with H2 in-memory database
   spring.application.name=university_GMS
   
   # H2 Database configuration
   spring.datasource.url=jdbc:h2:mem:testdb
   spring.datasource.driverClassName=org.h2.Driver
   spring.datasource.username=sa
   spring.datasource.password=password
   
   # JPA/Hibernate properties
   spring.jpa.database-platform=org.hibernate.dialect.H2Dialect
   spring.jpa.hibernate.ddl-auto=create-drop
   spring.jpa.show-sql=true
   
   # H2 Console (for development only)
   spring.h2.console.enabled=true
   ```

#### Running the Application

- **With development profile**:
  ```bash
  java -jar target/university_GMS-0.0.1-SNAPSHOT.jar --spring.profiles.active=dev
  ```
  - Application starts on port 8080
  - H2 console available at: http://localhost:8080/h2-console
  - Takes ~4-5 seconds to start. NEVER CANCEL startup processes.

- **Default startup** (will fail without production database):
  ```bash
  java -jar target/university_GMS-0.0.1-SNAPSHOT.jar
  ```
  - Requires PostgreSQL configuration or will fail with "Failed to determine a suitable driver class"

### Testing and Validation

#### Build Validation
Always run these validation steps after making changes:
1. `./mvnw clean compile` - Verify code compiles
2. `./mvnw test -Dspring.profiles.active=dev` - Run tests with H2 database
3. `java -jar target/university_GMS-0.0.1-SNAPSHOT.jar --spring.profiles.active=dev` - Verify application starts

#### Manual Application Testing
After making changes, ALWAYS test the following:
1. **Application Startup**: Verify application starts without errors
2. **Security**: Application has Spring Security enabled with generated password
3. **Database Connection**: H2 console should be accessible at `/h2-console`
4. **Logging**: Check startup logs for any warnings or errors

#### Expected Validation Output
- **Successful startup log patterns**:
  ```
  Started UniversityGmsApplication in X.XXX seconds
  Tomcat started on port 8080 (http)
  H2 console available at '/h2-console'
  Using generated security password: [password]
  ```

### Common Build Errors and Solutions

#### Java Version Errors
- **Error**: "release version 21 not supported"
- **Solution**: Ensure Java 21 is installed and JAVA_HOME is set correctly

#### Database Connection Errors
- **Error**: "Failed to determine a suitable driver class"
- **Solution**: Use development profile with H2 or configure PostgreSQL

#### Test Failures
- **Error**: "Failed to load ApplicationContext"
- **Solution**: Run tests with development profile: `-Dspring.profiles.active=dev`

### Repository Structure

#### Key Directories and Files
- **`src/main/java/com/nathan/university_gms/`** - Main application code
  - `UniversityGmsApplication.java` - Main Spring Boot application class
- **`src/test/java/com/nathan/university_gms/`** - Test code
  - `UniversityGmsApplicationTests.java` - Basic Spring context test
- **`src/main/resources/`** - Configuration files
  - `application.properties` - Main configuration
- **`pom.xml`** - Maven project configuration
- **`.github/`** - GitHub templates and documentation

#### Technology Stack
- **Spring Boot 3.5.6** with Java 21
- **Spring Data JPA** for database operations
- **Spring Security** for authentication/authorization
- **PostgreSQL** for production database
- **H2** for development/testing (when added)
- **Flyway** for database migrations
- **JWT** for token-based authentication
- **Spring Boot Mail** for email functionality
- **ModelMapper** for object mapping

#### Dependencies Overview
Key dependencies from pom.xml:
- Spring Boot Starter Web, Data JPA, Security, Validation
- PostgreSQL driver
- JWT libraries (jjwt-api, jjwt-impl, jjwt-jackson)
- Flyway for database migrations
- ModelMapper for object mapping
- Spring Boot Mail for email

### CI/CD and Automation

#### Existing CI
- Repository has CI workflow configured
- No workflows directory found in local clone but GitHub shows CI workflow exists

#### Development Workflow
1. Make code changes
2. Build and test locally: `./mvnw clean package -DskipTests`
3. Run tests: `./mvnw test -Dspring.profiles.active=dev`
4. Start application: Test with dev profile
5. Commit changes after validation

### Troubleshooting Common Issues

#### Build Issues
- **Maven Download Slow**: First build downloads dependencies, subsequent builds are faster
- **Compilation Errors**: Ensure Java 21 is properly configured

#### Runtime Issues
- **Port 8080 in use**: Stop other applications or change port via `--server.port=8081`
- **Database errors**: Verify H2 dependency and dev profile configuration

#### Development Tips
- Use `spring.profiles.active=dev` for all development work
- H2 console is valuable for debugging database issues
- Generated security password changes on each restart
- Spring Boot DevTools included for development hot reload

### Performance Expectations
- **Clean compile**: 3-5 seconds
- **Full package build**: 8-10 seconds  
- **Test execution**: 5-6 seconds
- **Application startup**: 4-5 seconds
- **First Maven run**: 20-30 seconds (downloads dependencies)

**CRITICAL**: NEVER CANCEL any build or test commands. All operations complete quickly but Maven may need time to download dependencies on first run.