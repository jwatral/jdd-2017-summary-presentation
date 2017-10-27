## JDD 2017 Summary

---

### Agenda for today

+++

- JDD 2017 Summary                          
- JVM9                                      |
- TOP10 security vulnerabilities in WebApps |
- NGNIX & Lua                               |

---

### What's new in the JAVA 9?

---

### What’s New for the Java Language in JDK 9?

+++

#### Not much really:
##### JEP 213: Milling Project Coin
- @SafeVarags on private instance methods |
- You can use diamond syntax in conjunction with anonymous inner classes |
- The underscore character is not a legal name |
- Private interface methods are supported |

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

+++

#### JEP 269: Convenience Factory Methods for Collections
     
```java
Set<String> set = new HashSet<>();
set.add("a");
set.add("b");
set.add("c");
set = Collections.unmodifiableSet(set);

Set<String> set = Collections.unmodifiableSet(new HashSet<>(Arrays.asList("a", "b", "c")));

Set<String> set = Collections.unmodifiableSet(new HashSet<String>() {{
    add("a"); add("b"); add("c");
}});

Set<String> set = Collections.unmodifiableSet(Stream.of("a", "b", "c").collect(toSet()));

Set<String> set = Set.of("a", "b", "c");
```

@[1-5](#facePalm)
@[7](#facePalm2)
@[9-11](#screamingDoubleFacePalm)
@[13](#stillFacePalm)
@[15](Well done JAVA... C# had this function since like... forever?)

---

### Key Changes in JDK 9

+++

#### Java Platform Module System (JSR 376)
- JEP 261: Module System |
- JEP 200: The Modular JDK |
- JEP 220: Modular Run-Time Images |
- JEP 260: Encapsulate Most Internal APIs |

Note:
module hell instead of classpath

+++

#### JEP 223: New Version-String Scheme
```
1.8.0_144-b01
```
##### VS.
```
$MAJOR.$MINOR.$SECURITY.$PATCH
```

---

## What’s New for Tools in JDK 9?

+++

- JEP 222: jshell: The Java Shell (Read-Eval-Print Loop)
- JEP 228: Add More Diagnostic Commands
- JEP 231: Remove Launch-Time JRE Version Selection
- **JEP 238: Multi-Release JAR Files**
- JEP 240: Remove the JVM TI hprof Agent
- JEP 241: Remove the jhat Tool	|
- **JEP 245: Validate JVM Command-Line Flag Arguments**
- JEP 247: Compile for Older Platform Versions
- JEP 282: jlink: The Java Linker

---

## What’s New for Security in JDK 9?

+++

- JEP 219: Datagram Transport Layer Security (DTLS)
- JEP 244: TLS Application-Layer Protocol Negotiation Extension
- JEP 249: OCSP Stapling for TLS
- JEP 246: Leverage CPU Instructions for GHASH and RSA
- **JEP 273: DRBG-Based SecureRandom Implementations**
- **JEP 288: Disable SHA-1 Certificates**
- **JEP 229: Create PKCS12 Keystores by Default**
- JEP 287: SHA-3 Hash Algorithms

Note:
JEP 273: DRBG-Based SecureRandom Implementations	
Provides the functionality of Deterministic Random Bit Generator (DRBG) mechanisms as specified in NIST SP 800-90Ar1 in the SecureRandom API.
The DRBG mechanisms use modern algorithms as strong as SHA-512 and AES-256. Each of these mechanisms can be configured with different security strengths and features to match user requirements.
See Generating Random Numbers in Java Platform, Standard Edition Security Developer's Guide.

JEP 288: Disable SHA-1 Certificates
Improves the security configuration of the JDK by providing a more flexible mechanism to disable X.509 certificate chains with SHA-1-based signatures.
Disables SHA-1 in TLS Server certificate chains anchored by roots included by default in the JDK; local or enterprise certificate authorities (CAs) are not affected.
The jdk.certpath.disabledAlgorithms security property is enhanced with several new constraints that allow greater control over the types of certificates that can be disabled.

JEP 229: Create PKCS12 Keystores by Default
Modifies the default keystore type from JKS to PKCS12. PKCS#12 is an extensible, standard, and widely supported format for storing cryptographic keys. PKCS12 keystores improve confidentiality by storing private keys, trusted public key certificates, and secret keys. This feature also opens opportunities for interoperability with other systems such as Mozilla, Microsoft's Internet Explorer, and OpenSSL that support PKCS12.

---

## What’s New for Javadoc in JDK 9?

+++

- JEP 221: Simplified Doclet API	
- **JEP 224: HTML5 Javadoc**
- JEP 225: Javadoc Search	
- JEP 261: Module System

---

## And now's the time for more interesting changes!

---

## What’s New for the JVM in JDK 9

+++

- JEP 165: Compiler Control
- JEP 197: Segmented Code Cache	
- JEP 276: Dynamic Linking of Language-Defined Object Models

---

## What’s New for JVM Tuning in JDK 9

+++

- Improve G1 Usability, Determinism, and Performance	
- JEP 158: Unified JVM Logging	
- JEP 214: Remove GC Combinations Deprecated in JDK 8	
- **JEP 248: Make G1 the Default Garbage Collector**
- JEP 271: Unified GC Logging	
- JEP 291: Deprecate the Concurrent Mark Sweep (CMS) Garbage Collector

---

## What’s New for Core Libraries in JDK 9?

---

## And remember:
>New is always better!

<span style="font-size:0.6em; color:gray; float:right;">Barney Stinson</span>



