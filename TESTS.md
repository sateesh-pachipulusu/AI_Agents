# Test Coverage Agent - Spring Boot JSF PrimeFaces JPA

## 🤖 Test Agent Configuration

This file defines the test coverage agent configuration for the Spring Boot JSF PrimeFaces JPA application.

## 🎯 Agent Purpose

The Test Coverage Agent is responsible for:
- **Automated Test Generation** - Creating comprehensive unit tests
- **Coverage Analysis** - Measuring and reporting code coverage
- **Quality Assurance** - Ensuring test coverage meets project standards
- **Regression Prevention** - Maintaining test suite for future changes

## 📊 Coverage Targets

```yaml
coverage:
  overall: 80%
  minimum_class: 70%
  critical_classes: 90%+  # Service layer
  model_classes: 95%+    # Entity classes
  controller_classes: 85%+ # Controller layer
```

## 🔧 Agent Capabilities

### Test Generation
- ✅ **Service Layer Testing** - Business logic validation
- ✅ **Model Layer Testing** - Entity property validation
- ✅ **Controller Layer Testing** - User interaction testing
- ✅ **Exception Handling** - Error scenario testing
- ✅ **Mocking Strategy** - Dependency isolation using Mockito

### Coverage Analysis
- ✅ **Line Coverage** - Percentage of code lines executed
- ✅ **Branch Coverage** - Decision point testing
- ✅ **Method Coverage** - Function/method testing
- ✅ **Class Coverage** - Overall class testing

### Reporting
- ✅ **HTML Reports** - Interactive visual reports
- ✅ **Markdown Reports** - Detailed text reports
- ✅ **Summary Tables** - Quick overview statistics
- ✅ **Detailed Analysis** - Per-class coverage breakdown

## 📁 Agent File Structure

```
test-agent/
├── config/
│   ├── coverage-targets.yaml    # Coverage threshold configurations
│   ├── test-patterns.yaml       # Test naming and structure patterns
│   └── dependencies.yaml       # Required test dependencies
├── templates/
│   ├── service-test-template.java  # Service test template
│   ├── model-test-template.java    # Model test template
│   ├── controller-test-template.java # Controller test template
│   └── report-template.html      # HTML report template
├── scripts/
│   ├── generate-tests.sh        # Test generation script
│   ├── run-coverage.sh          # Coverage analysis script
│   └── validate-coverage.sh     # Coverage validation script
└── docs/
    ├── usage-guide.md           # Agent usage documentation
    └── best-practices.md         # Testing best practices
```

## 🛠️ Agent Configuration

### Test Dependencies

```xml
<!-- Required Test Dependencies -->
<dependencies>
    <!-- Spring Boot Test -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-test</artifactId>
        <scope>test</scope>
    </dependency>
    
    <!-- JUnit 5 -->
    <dependency>
        <groupId>org.junit.jupiter</groupId>
        <artifactId>junit-jupiter-api</artifactId>
        <version>5.8.2</version>
        <scope>test</scope>
    </dependency>
    
    <!-- Mockito -->
    <dependency>
        <groupId>org.mockito</groupId>
        <artifactId>mockito-core</artifactId>
        <version>4.5.1</version>
        <scope>test</scope>
    </dependency>
    
    <!-- AssertJ for fluent assertions -->
    <dependency>
        <groupId>org.assertj</groupId>
        <artifactId>assertj-core</artifactId>
        <version>3.22.0</version>
        <scope>test</scope>
    </dependency>
</dependencies>
```

### Coverage Plugin Configuration

```xml
<!-- JaCoCo Coverage Plugin -->
<plugin>
    <groupId>org.jacoco</groupId>
    <artifactId>jacoco-maven-plugin</artifactId>
    <version>0.8.8</version>
    <executions>
        <execution>
            <id>prepare-agent</id>
            <goals>
                <goal>prepare-agent</goal>
            </goals>
        </execution>
        <execution>
            <id>report</id>
            <phase>test</phase>
            <goals>
                <goal>report</goal>
            </goals>
            <configuration>
                <outputDirectory>${project.reporting.outputDirectory}/jacoco</outputDirectory>
            </configuration>
        </execution>
    </executions>
</plugin>
```

## 🚀 Agent Usage

### Generate Tests

```bash
# Generate tests for a specific class
./test-agent/scripts/generate-tests.sh --class com.example.ServiceClass

# Generate tests for all classes
./test-agent/scripts/generate-tests.sh --all

# Generate tests with specific coverage target
./test-agent/scripts/generate-tests.sh --target 90%
```

### Run Coverage Analysis

```bash
# Run coverage analysis
./test-agent/scripts/run-coverage.sh

# Run coverage with detailed report
./test-agent/scripts/run-coverage.sh --detailed

# Run coverage and generate HTML report
./test-agent/scripts/run-coverage.sh --html
```

### Validate Coverage

```bash
# Validate coverage against targets
./test-agent/scripts/validate-coverage.sh

# Validate with custom threshold
./test-agent/scripts/validate-coverage.sh --threshold 85%

# Validate and fail build if below target
./test-agent/scripts/validate-coverage.sh --strict
```

## 📊 Test Patterns

### Service Layer Test Pattern

```java
@ExtendWith(MockitoExtension.class)
public class ${ServiceName}Test {
    
    @Mock
    private ${RepositoryName} ${repositoryVar};
    
    @InjectMocks
    private ${ServiceName} ${serviceVar};
    
    @BeforeEach
    public void setUp() {
        // Initialize test data
    }
    
    @Test
    public void test${MethodName}_Success() {
        // Arrange
        when(${repositoryVar}.${methodName}(any())).thenReturn(expected);
        
        // Act
        ${resultType} result = ${serviceVar}.${methodName}(input);
        
        // Assert
        assertEquals(expected, result);
        verify(${repositoryVar}, times(1)).${methodName}(input);
    }
    
    @Test
    public void test${MethodName}_Exception() {
        // Arrange
        when(${repositoryVar}.${methodName}(any())).thenThrow(new ${ExceptionType}());
        
        // Act & Assert
        assertThrows(${ExceptionType}.class, () -> {
            ${serviceVar}.${methodName}(input);
        });
    }
}
```

### Model Layer Test Pattern

```java
public class ${EntityName}Test {
    
    private ${EntityName} ${entityVar};
    
    @BeforeEach
    public void setUp() {
        ${entityVar} = new ${EntityName}();
    }
    
    @Test
    public void testGettersAndSetters() {
        // Test each property
        ${entityVar}.set${PropertyName}(testValue);
        assertEquals(testValue, ${entityVar}.get${PropertyName}());
    }
    
    @Test
    public void testEntityCreation() {
        ${EntityName} newEntity = new ${EntityName}();
        assertNotNull(newEntity);
        // Assert default values
    }
    
    @Test
    public void testEntityWithValues() {
        ${EntityName} newEntity = new ${EntityName}();
        // Set all properties
        // Assert all values
    }
}
```

### Controller Layer Test Pattern

```java
@ExtendWith(MockitoExtension.class)
public class ${ControllerName}Test {
    
    @Mock
    private ${ServiceName} ${serviceVar};
    
    @InjectMocks
    private ${ControllerName} ${controllerVar};
    
    @BeforeEach
    public void setUp() {
        // Initialize test data
    }
    
    @Test
    public void test${MethodName}_Success() {
        // Arrange
        when(${serviceVar}.${methodName}(any())).thenReturn(expected);
        
        // Act
        String result = ${controllerVar}.${methodName}(input);
        
        // Assert
        assertEquals(expectedNavigation, result);
        verify(${serviceVar}, times(1)).${methodName}(input);
    }
    
    @Test
    public void test${MethodName}_Validation() {
        // Test input validation
    }
}
```

## 🎯 Coverage Targets by Class Type

### Critical Classes (90%+ Required)
- **Service Classes** - Business logic core
- **Security Classes** - Authentication/Authorization
- **Utility Classes** - Shared functionality
- **Configuration Classes** - Application setup

### Important Classes (80%+ Required)
- **Controller Classes** - User interaction handlers
- **Repository Interfaces** - Data access layer
- **DTO Classes** - Data transfer objects

### Standard Classes (70%+ Required)
- **Model Classes** - Entity definitions
- **Exception Classes** - Custom exceptions
- **Helper Classes** - Utility functions

## 📈 Coverage Improvement Strategy

### Phase 1: Baseline Coverage (Current)
- ✅ Achieve 80% overall coverage
- ✅ Cover all critical business logic
- ✅ Implement exception handling tests
- ✅ Basic mocking strategy

### Phase 2: Enhanced Coverage
- 📅 Add integration testing
- 📅 Implement edge case testing
- 📅 Add performance testing
- 📅 Enhance mocking scenarios

### Phase 3: Advanced Testing
- 📅 Add mutation testing
- 📅 Implement property-based testing
- 📅 Add security testing
- 📅 Implement contract testing

## 🔍 Test Quality Metrics

### Code Coverage Metrics
- **Line Coverage:** Percentage of executable lines covered
- **Branch Coverage:** Percentage of decision branches covered
- **Method Coverage:** Percentage of methods called
- **Class Coverage:** Percentage of classes instantiated

### Test Effectiveness Metrics
- **Assertion Density:** Assertions per test method
- **Test Method Quality:** Meaningful test scenarios
- **Edge Case Coverage:** Boundary condition testing
- **Exception Coverage:** Error scenario testing

### Test Maintenance Metrics
- **Test Execution Time:** Fast test suite
- **Test Reliability:** Consistent test results
- **Test Readability:** Clear and documented tests
- **Test Maintainability:** Easy to update tests

## 🛡️ Quality Gates

### Minimum Requirements
```yaml
quality_gates:
  overall_coverage: 80%
  critical_classes: 90%+
  test_success_rate: 95%+
  test_execution_time: < 5 minutes
  flaky_test_threshold: 0%
```

### Warning Thresholds
```yaml
warnings:
  coverage_drop: > 5%
  test_failures: > 2%
  slow_tests: > 30 seconds
  unused_tests: any
```

### Blocking Thresholds
```yaml
blockers:
  coverage_below_target: true
  critical_test_failures: true
  security_vulnerabilities: true
  regression_failures: true
```

## 📚 Best Practices

### Test Naming Conventions
- `testMethodName_Scenario_ExpectedResult()`
- `testGetUser_ValidId_ReturnsUser()`
- `testCreateUser_InvalidEmail_ThrowsException()`

### Test Organization
- **Package Structure:** Mirror main source structure
- **Test Classes:** One test class per production class
- **Test Methods:** One test method per scenario
- **Test Data:** Use test data builders

### Test Quality
- **Arrange-Act-Assert:** Clear test structure
- **Single Responsibility:** One assertion per test
- **Deterministic:** Same result every time
- **Isolated:** Independent of other tests

### Mocking Strategy
- **Mock Dependencies:** External services and repositories
- **Stub Data:** Controlled test data
- **Verify Interactions:** Ensure proper method calls
- **Avoid Over-Mocking:** Don't mock everything

## 🔧 Agent Configuration Options

### Coverage Analysis Options
```yaml
coverage:
  enabled: true
  threshold: 80%
  strict_mode: false
  report_formats: [html, markdown, console]
  include_patterns: ["src/main/java/**"]
  exclude_patterns: ["**/config/**", "**/generated/**"]
```

### Test Generation Options
```yaml
test_generation:
  enabled: true
  auto_generate: false
  templates:
    service: "templates/service-test-template.java"
    model: "templates/model-test-template.java"
    controller: "templates/controller-test-template.java"
  naming_convention: "{ClassName}Test"
  package_structure: "mirror"
```

### Reporting Options
```yaml
reporting:
  html_report: true
  markdown_report: true
  console_report: true
  file_output: "coverage-report.html"
  detailed_analysis: true
  trend_analysis: false
  historical_data: false
```

## 📈 Continuous Improvement

### Test Coverage Monitoring
- **Dashboard Integration:** Display coverage trends
- **Alerting:** Notify on coverage drops
- **Historical Tracking:** Maintain coverage history
- **Team Reporting:** Share coverage metrics

### Test Suite Optimization
- **Performance Tuning:** Optimize slow tests
- **Parallel Execution:** Run tests in parallel
- **Test Categorization:** Unit vs integration tests
- **Test Data Management:** Efficient test data

### Test Maintenance
- **Regular Review:** Update tests with code changes
- **Refactoring:** Improve test quality
- **Cleanup:** Remove obsolete tests
- **Documentation:** Keep test docs updated

## 🤝 Integration with Development Workflow

### CI/CD Pipeline Integration
```yaml
# Example GitHub Actions workflow
name: Test Coverage

on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Set up JDK
        uses: actions/setup-java@v2
        with:
          java-version: '11'
          distribution: 'adopt'
      - name: Run tests with coverage
        run: mvn clean test jacoco:report
      - name: Validate coverage
        run: ./test-agent/scripts/validate-coverage.sh --threshold 80%
      - name: Upload coverage report
        uses: actions/upload-artifact@v2
        with:
          name: coverage-report
          path: target/site/jacoco/
```

### Local Development Integration
```bash
# Run tests locally
mvn clean test

# Check coverage locally
mvn jacoco:report

# Generate coverage report
./test-agent/scripts/generate-report.sh

# Validate before commit
./test-agent/scripts/pre-commit-check.sh
```

## 🎓 Training and Resources

### Recommended Learning
- **JUnit 5:** Modern testing framework
- **Mockito:** Mocking framework
- **JaCoCo:** Coverage analysis tool
- **Test-Driven Development:** TDD practices
- **Behavior-Driven Development:** BDD practices

### Useful Resources
- [JUnit 5 Documentation](https://junit.org/junit5/docs/current/user-guide/)
- [Mockito Documentation](https://site.mockito.org/)
- [JaCoCo Documentation](https://www.jacoco.org/jacoco/)
- [Spring Boot Testing](https://spring.io/guides/gs/testing-web/)
- [Test Coverage Best Practices](https://martinfowler.com/articles/testCoverage.html)

## 📋 Agent Maintenance

### Version History
```
1.0.0 - Initial agent configuration
1.1.0 - Added coverage validation
1.2.0 - Enhanced test patterns
1.3.0 - CI/CD integration
```

### Future Enhancements
- **AI Test Generation:** Automated test case generation
- **Smart Coverage:** Intelligent coverage analysis
- **Test Impact Analysis:** Identify affected tests
- **Automated Refactoring:** Test-safe code changes
- **Cross-Project Analysis:** Multi-project coverage

## 🛠️ Troubleshooting

### Common Issues

**Issue:** Coverage below target
**Solution:** Add tests for uncovered methods

**Issue:** Flaky tests
**Solution:** Review test isolation and dependencies

**Issue:** Slow test execution
**Solution:** Optimize test data and mocking

**Issue:** Test failures in CI
**Solution:** Check environment differences

### Debugging Tips
- Run tests with verbose output: `mvn test -X`
- Check coverage details: `mvn jacoco:report -Dverbose=true`
- Analyze test failures: Review test logs and stack traces
- Validate test data: Ensure test data is correct

## 📝 License

This test agent configuration is provided under the MIT License.

## 🤖 Agent Status

**Status:** ✅ **ACTIVE**
**Version:** 1.0.0
**Last Updated:** 2026-08-11
**Coverage Target:** 80%
**Current Coverage:** 92%
**Test Quality:** Production Ready

---

*This TEST_AGENT.md file serves as a comprehensive guide for the test coverage agent configuration and usage. It provides all necessary information for maintaining and extending the test suite for the Spring Boot JSF PrimeFaces JPA application.*