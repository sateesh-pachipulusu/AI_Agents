# Java Migration Agent Configuration

## Java Migration Analyzer Agent

### Agent Name: `java-migration-analyzer`

### Description
Analyzes Java codebase for target version upgrade readiness and outputs an HTML report without editing code. Expects user to specify source and target Java versions.

### Configuration

```yaml
name: java-migration-analyzer
description: >
  Analyzes Java codebase for target version upgrade readiness and outputs an HTML report without editing code.
  Expects user to specify source and target Java versions for flexible migration analysis.
user-invocable: true

# STRICT EXECUTION RULES
rules:
  - READ-ONLY OPERATION: DO NOT modify, move, or delete any source files, build scripts (pom.xml, build.gradle), or configuration files in the project.
  - OUTPUT REQUIREMENT: Produce a single, self-contained HTML file named java-migration-report.html in the current root directory.
  - USER INPUT: Expect source and target Java versions from user for flexible analysis.

# ANALYSIS SCOPE
analysis_scope:
  - Removed & Deprecated APIs:
    - Usage of sun.misc.BASE64Encoder / sun.misc.BASE64Decoder (replace with java.util.Base64)
    - Standard APIs removed or replaced (e.g., Thread.stop(), SecurityManager)
    - Deprecated GC options or VM flags
    - Version-specific API changes based on user input
  
  - EE to Jakarta Migration:
    - javax.* imports to jakarta.* (especially for Servlets, JPA, JAXB, JAX-WS)
    - Dependencies needing major version bumps (e.g., Spring Framework 5 -> 6, Spring Boot 2 -> 3)
    - Version-specific Jakarta EE requirements
  
  - Reflection & Strong Encapsulation (JEP 403):
    - Deep reflection access to JDK internals (requires --add-opens or library updates)
    - Version-specific encapsulation changes
  
  - Build & Dependency Analysis:
    - Incompatible Maven/Gradle plugins or outdated library versions (e.g., Lombok, ByteBuddy, ASM, Mockito)
    - Version-specific dependency compatibility
  
  - Modernization Opportunities:
    - Code patterns candidate for Records, Sealed Classes, Pattern Matching, Switch Expressions, and Virtual Threads
    - Version-specific feature recommendations
    - java.lang.Thread.ofVirtual() for Java 21+

# REPORT GENERATION FORMAT
report_format:
  - Dashboard: High-level summary cards (Total Files Scanned, Critical Blockers, Modernization Candidates, Estimated Effort)
  - Categorized Findings Table: Severity (CRITICAL, WARNING, INFO), File Path, Line Number, Detected Issue, Recommended Fix
  - Dependency Matrix: Deprecated libraries vs. target version compatible versions
  - Embedded CSS: Modern responsive styling (clean dark/light theme, flexbox/grid layout)
  - Version-Specific Recommendations: Tailored to user's target Java version

# SUPPORTED JAVA VERSIONS
supported_versions:
  from: 8
  to: 21
  note: Agent can analyze migrations between any supported versions based on user input

# USER INPUT REQUIREMENTS
user_input:
  required:
    - source_version: Source Java version (e.g., 8, 11)
    - target_version: Target Java version (e.g., 17, 21)
  optional:
    - project_name: Custom project name for report
    - focus_areas: Specific areas to focus on (e.g., "dependencies", "modernization")

# OUTPUT FILE
output:
  filename: java-migration-report.html
  format: HTML
  location: project_root
  naming_convention: "java{source_version}-to-{target_version}-migration-report.html"

# ANALYSIS CAPABILITIES
capabilities:
  - Java source code analysis
  - Dependency tree analysis
  - API compatibility checking
  - Modernization opportunity identification
  - HTML report generation
  - Responsive CSS styling
  - Version-specific migration analysis
  - Customizable report generation

# LIMITATIONS
limitations:
  - Read-only operation only
  - No code modification
  - No automatic fixes
  - Report generation only
  - Requires manual implementation of recommendations
  - Limited to supported Java versions (8-21)

# USAGE
usage:
  The agent analyzes the Java codebase and generates a comprehensive migration report
  highlighting compatibility issues and modernization opportunities when upgrading
  from a specified source Java version to a target Java version.

# EXAMPLE INVOCATIONS
example_invocation:
  - "Please analyze this Java 8 codebase for Java 17 migration readiness and generate a report."
  - "Analyze migration from Java 11 to Java 21 and create a detailed migration report."
  - "Generate Java migration report for upgrading from version 8 to version 21."

# EXAMPLE OUTPUT STRUCTURE
output_structure:
  - Executive Summary (with version-specific assessment)
  - Critical Issues (🔴) - version-specific blockers
  - High Priority Issues (🟠) - version-specific priorities
  - Medium Priority Issues (🟡) - version-specific considerations
  - Modernization Opportunities (🟢) - version-specific features
  - Dependency Migration Matrix - version-specific targets
  - Migration Strategy - version-specific approach
  - Risk Assessment - version-specific challenges
  - Summary Statistics - version-specific metrics
  - Recommendations - version-specific guidance

# AGENT BEHAVIOR
behavior:
  - Comprehensive codebase scanning
  - Detailed issue categorization
  - Actionable recommendations
  - Professional HTML reporting
  - Responsive design for all devices
  - Version-specific analysis based on user input
  - Dynamic report generation with custom naming

## Agent Invocation

To use this agent, specify the source and target Java versions for migration analysis:

```
Please analyze this Java 8 codebase for Java 17 migration readiness and generate a comprehensive report.
```

or

```
Analyze migration from Java 11 to Java 21 and create a detailed migration report.
```

## Expected Output

The agent will generate a `java{source_version}-to-{target_version}-migration-report.html` file in the project root directory containing:

- **Dashboard**: Key metrics at a glance (version-specific)
- **Issue Analysis**: Categorized by severity with remediation guidance
- **Dependency Matrix**: Current vs target versions (version-specific)
- **Migration Strategy**: Step-by-step approach (version-specific)
- **Modernization Opportunities**: Target version features to leverage
- **Risk Assessment**: Version-specific challenges and mitigations
- **Version-Specific Recommendations**: Tailored to your migration path

## Compatibility Notes

This agent configuration supports flexible Java version migration analysis and can be adapted for various migration scenarios:

- **Supported Migration Paths**: Java 8→11, 8→17, 8→21, 11→17, 11→21, 17→21
- **Framework Support**: Spring Boot, JSF, PrimeFaces, JPA applications
- **Customization**: Can be adapted for other Java applications with similar dependency structures

## User Input Flexibility

The agent expects user to specify:
- **Source Java Version**: Current version (e.g., 8, 11)
- **Target Java Version**: Desired version (e.g., 17, 21)
- **Optional Parameters**: Project name, focus areas

This allows for customized migration analysis tailored to your specific upgrade requirements.