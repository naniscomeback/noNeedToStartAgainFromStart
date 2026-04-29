# Java Decision-Making & Control Flow Guide

This guide outlines architectural best practices for writing clean, readable, and maintainable Java code by replacing complex nested structures with efficient control flow patterns.

---

## 1. The Guard Clause Pattern
Avoid deep nesting (the "Arrow" anti-pattern). Instead, use Guard Clauses to check for failure cases first and exit early. This keeps the "happy path" flat and readable.

**Poor (Nested):**
```java
if (user != null) {
    if (user.isActive()) {
        if (user.hasPermission("ADMIN")) {
            // Do logic
        }
    }
}
```
**Senior:**
```java
if (user == null || !user.isActive()) return;
if (!user.hasPermission("ADMIN")) throw new SecurityException("Unauthorized");

// The happy path is un-indented and easy to follow
executeAdminLogic(user);
```
