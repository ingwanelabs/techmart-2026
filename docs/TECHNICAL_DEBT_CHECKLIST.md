# Technical Debt Audit Checklist

Use this checklist to systematically audit the TechMart sales pipeline codebase. For each item you find, document it in your Technical Debt Register.

## Code Quality

### Hard-coded Values
- [ ] Hard-coded database names or server addresses
- [ ] Hard-coded file paths (not using relative paths or configuration)
- [ ] Hard-coded date ranges or time periods
- [ ] Magic numbers without explanation (thresholds, limits, constants)
- [ ] Hard-coded credentials or API keys

### Code Duplication
- [ ] Same SQL query repeated in multiple places
- [ ] Same subquery used multiple times instead of using a CTE or view
- [ ] Repeated code blocks that could be extracted into functions
- [ ] Copy-pasted logic with minor variations

### Naming and Readability
- [ ] Unclear or cryptic variable names (e.g., `c`, `r`, `df`)
- [ ] Inconsistent naming conventions
- [ ] Poor or missing comments on complex logic
- [ ] Deeply nested code that's hard to follow
- [ ] Cryptic table aliases that don't aid understanding

---

## Performance Issues

### Database Performance
- [ ] `SELECT *` instead of specific columns
- [ ] Functions applied to columns in WHERE clauses (prevents index usage)
- [ ] Nested subqueries instead of CTEs or JOINs
- [ ] Missing or inappropriate indexes (check query patterns)
- [ ] Inefficient JOINs or Cartesian products
- [ ] Repeated queries that could be combined

### Application Performance
- [ ] Reading entire files into memory without streaming
- [ ] Inefficient loops or data processing
- [ ] Unnecessary data conversions or transformations
- [ ] Missing batch processing for large datasets

---

## Security Issues

### Credentials and Secrets
- [ ] Passwords stored in plain text
- [ ] Credentials committed to version control
- [ ] Connection strings with embedded passwords
- [ ] API keys or tokens in code or config files
- [ ] Email passwords or SMTP credentials exposed

### SQL Injection Risk
- [ ] Dynamic SQL constructed with string concatenation
- [ ] User input not parameterized
- [ ] Lack of input validation

### Data Protection
- [ ] Sensitive data (PII, card numbers) not masked in logs or output
- [ ] Missing encryption for sensitive data
- [ ] Over-permissive database access

---

## Maintainability

### Documentation
- [ ] Missing or outdated README
- [ ] No inline comments explaining complex logic
- [ ] Undocumented assumptions about data or business rules
- [ ] No documentation of known issues or limitations
- [ ] Missing usage examples or setup instructions

### Error Handling
- [ ] No try-catch blocks or error handling
- [ ] Database operations without transaction management
- [ ] Missing validation before INSERT/UPDATE operations
- [ ] No NULL handling in SQL queries
- [ ] Silent failures (errors not logged or reported)

### Code Structure
- [ ] Long functions that do too much (lack of single responsibility)
- [ ] Commented-out code left in files
- [ ] TODO comments that are never addressed
- [ ] Mixing concerns (e.g., business logic in database queries)

---

## Configuration Management

### Dependencies
- [ ] Outdated library versions with known security vulnerabilities
- [ ] Deprecated functions or syntax still in use
- [ ] Missing version pinning in requirements
- [ ] Unused dependencies listed

### Environment Configuration
- [ ] Environment-specific values hard-coded (not using environment variables)
- [ ] No separation between dev/test/production configuration
- [ ] Configuration mixed with code instead of external files
- [ ] Lack of configuration validation on startup

---

## Logging and Monitoring

- [ ] Missing logging for critical operations
- [ ] No audit trail for data changes
- [ ] No monitoring or alerting hooks
- [ ] Print statements instead of proper logging
- [ ] No performance metrics or instrumentation

---

## How to Use This Checklist

1. **Work through each category systematically** - don't try to spot everything at once
2. **Check each file against relevant items** - not all items apply to all files
3. **Document findings in your Technical Debt Register** - record what you find, where it is, and why it matters
4. **Use line numbers** - be specific about locations
5. **Consider impact** - not all technical debt is equal

Remember: The goal isn't to find every possible issue, but to develop your ability to spot common patterns of technical debt and assess their priority.
