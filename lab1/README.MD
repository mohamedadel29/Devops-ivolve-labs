# Lab 1: Building and Packaging Java Application with Gradle

## Objective

This lab demonstrates how to build, test, package, and run a Java application using Gradle.

---

## Prerequisites

- Java JDK
- Gradle
- Git

---

## Step 1: Install Gradle

Verify Gradle installation.

```bash
gradle -v
```

---

## Step 2: Clone the Repository

```bash
git clone https://github.com/Ibrahim-Adel15/calculator-gradle.git
```

Move to the project directory.

```bash
cd calculator-gradle
```

---

## Step 3: Run Unit Tests

Execute the unit tests.

```bash
gradle test
```

### Output

<img src="https://github.com/mohamedadel29/Devops-ivolve-labs/blob/main/images/gradle-test.png?raw=true" width="900">

---

## Step 4: Build the Application

Generate the executable JAR file.

```bash
gradle build
```

Verify that the artifact has been created.

```bash
ls build/libs/
```

Expected output:

```
calculator.jar
```

### Output

<img src="https://github.com/mohamedadel29/Devops-ivolve-labs/blob/main/images/gradle-build.png?raw=true" width="900">

---

## Step 5: Run the Application

Execute the generated JAR file.

```bash
java -jar build/libs/calculator.jar
```

Example:

```
Enter first number: 5
Enter second number: 2

Sum: 7.0
Subtract: 3.0
Multiply: 10.0
Divide: 2.5
```

### Output

<img src="https://github.com/mohamedadel29/Devops-ivolve-labs/blob/main/images/run-app.png?raw=true" width="900">

---

## Verification

The application executed successfully and produced the expected arithmetic results.

- ✅ Unit tests passed.
- ✅ Build completed successfully.
- ✅ `calculator.jar` generated in `build/libs/`.
- ✅ Application ran successfully.