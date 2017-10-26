## JDD 2017 Summary

---

### Agenda for today

+++

- JDD 2017 Summary                          
- JVM9                                      |
- TOP10 security vulnerabilities in WebApps |
- NGNIX & Lua                               |

---

### What's new in the JVM9?

---

### From code's POV

+++

#### Not much really:
- @SafeVarags on private instance methods |
- You can use diamond syntax in conjunction with anonymous inner classes |
- The underscore character is not a legal name |
- Private interface methods are supported

+++ 

#### More Concise try-with-resources Statements

```java
final Resource resource1 = new Resource("resource1");
Resource resource2 = new Resource("resource2");

try (Resource r1 = resource1;
     Resource r2 = resource2) {
    ...
}

try (resource1;
     resource2) {
    ...
}
```

@[1](A final resource)
@[2](An effectively final resource)
@[3-7](Old way)
@[9-13](New and improved try-with-resources statement in Java SE 9)

---

# Numbers

- 1 |
- 2 |
- 3 |

---

# Letters

- A |
- B |
- C |

---

# Metavariables

- Foo |
- Bar |
- Baz |

---