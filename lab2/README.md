# Lab 2: Building and Packaging Java Application with Maven

## Objective

This lab demonstrates how to build, test, package, and run a Java application using Apache Maven.

---

## Prerequisites

- Java JDK
- Apache Maven
- Git

---

## Step 1: Install Maven

Verify Maven installation.

```bash
mvn -version
```

---

## Step 2: Clone the Repository

```bash
git clone https://github.com/Ibrahim-Adel15/calculator-maven.git
```

Navigate to the project directory.

```bash
cd calculator-maven
```

---

## Step 3: Run Unit Tests

Execute the unit tests.

```bash
mvn test
```

### Output

<img src="./images/maven-test.png" width="900">

---

## Step 4: Build the Application

Generate the executable JAR file.

```bash
mvn clean package
```

Verify that the artifact has been created.

```bash
ls target/
```

Expected output:

```text
calculator.jar
```

### Output

<img src="./images/maven-build.png" width="900">

---

## Step 5: Run the Application

Execute the generated JAR file.

```bash
java -jar target/calculator.jar
```

Example:

```text
Enter first number: 5
Enter second number: 5

Sum: 10.0
Subtract: 0.0
Multiply: 25.0
Divide: 1.0
```

### Output

<img src="./images/run-app2.png" width="900">

---

## Verification

The application executed successfully and produced the expected arithmetic results.

- ✅ Unit tests passed successfully.
- ✅ Build completed successfully.
- ✅ `calculator.jar` was generated inside the `target/` directory.
- ✅ Application ran successfully and produced the expected output.