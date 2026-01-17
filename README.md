# TestLang++ Compiler

A Domain-Specific Language (DSL) for HTTP API testing that compiles to JUnit 5 tests.

##  Quick Start Guide

### Prerequisites
- Java 11 or higher
- Maven 3.6+
- Spring Boot Backend running on port 8080

---

## 1. How to Run the Backend

### Start the Backend:
1. Open the `demobackend` project in IntelliJ
2. In Maven panel, click **`spring-boot:run`** (under Plugins → spring-boot)
3. Wait for: `Started TestLangBackendApplication in X.XXX seconds`

**Backend is now running on:** `http://localhost:8080`

**Available Endpoints:**
- `POST /api/login` - User authentication with username/password
- `GET /api/users/{id}` - Retrieve user information
- `PUT /api/users/{id}` - Update user data

**Test Data:**
- **Valid login**: `{"username":"admin","password":"1234"}`
- **Valid user ID**: `42`

**Keep the backend running** while testing!


## 2. How to Run the Parser (Using Maven Control Panel)

### Step 1: Build the Compiler
1. Open **Maven panel** in IntelliJ
2. Expand your project → **Lifecycle**
3. Click **`clean`** (wait for completion)
4. Click **`compile`** (wait for "BUILD SUCCESS")

This generates:
- `Lexer.java` from `testlang.flex` (JFlex)
- `parser.java` from `parser.cup` (CUP)
- Compiles all Java sources

## Step 3: Run the Parser (Valid Tests)
1. Create **Run Configuration** for `Main.java`
2. Set **Program arguments**: `example.test GeneratedTests.java`
3. Click **Run**

**Expected Output:**
Parsing: example.test
Found 4 test(s)
Found 3 variable(s)
Successfully generated: GeneratedTests.java

## 4. How to Run Generated Tests (Using Maven Control Panel)

### Run All Tests:
1. Make sure **backend is running**
2. In Maven panel, click **`test`** (under Lifecycle)

**Expected Output:**
✅ Login - ALL ASSERTIONS PASSED
✅ GetUser - ALL ASSERTIONS PASSED  
✅ RangeCheck - ALL ASSERTIONS PASSED
✅ BothSyntaxes - ALL ASSERTIONS PASSED

Tests run: 4, Failures: 0, Errors: 0, Skipped: 0
BUILD SUCCESS


## 5. How to Test Error Handling 

### Step 1: Create Error Configuration
1. Create Run Configuration named "Show Error"
2. Set Main class: com.testlang.Main
3. Set Program arguments: invalid.test ErrorOutput.java

### Step 2: Run Error Test
1. Ensure invalid.test file exists with invalid syntax:
2. Run the "Show Error" configuration
3. 
   **Expected Output:**
   Parsing: invalid.test
   Syntax error at character 3 of input
   Couldn't repair and continue parse at character X of input
   Error: Can't recover from previous error(s)
