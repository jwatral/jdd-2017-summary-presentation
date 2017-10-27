## JDD 2017 Summary

---

### Agenda for today

+++

- JDD 2017 Summary                          |
- JVM9                                      |
- TOP10 security vulnerabilities in WebApps |
- NGNIX & Lua*                              |

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

## What’s New for Internationalization in JDK 9?

+++

- JEP 267: Unicode 8.0	
- JEP 252: CLDR Locale Data Enabled by Default	
- JEP 226: UTF-8 Properties Files

---

## And the last bunch of "boring" changes:
## What’s New for Client Technologies in JDK 9

+++

- JEP 251: Multi-Resolution Images	
- JEP 253: Prepare JavaFX UI Controls and CSS APIs for Modularization	
- JEP 256: BeanInfo Annotations	
- JEP 262: TIFF Image I/O	
- JEP 263: HiDPI Graphics on Windows and Linux	
- JEP 272: Platform-Specific Desktop Features	
- JEP 283: Enable GTK 3 on Linux	

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

+++

- JEP 102: Process API Updates	
- JEP 193: Variable Handles	
- **JEP 254: Compact Strings**	
- JEP 264: Platform Logging API and Service	
- JEP 266: More Concurrency Updates	
- JEP 268: XML Catalogs	
- **JEP 269: Convenience Factory Methods for Collections**
- JEP 274: Enhanced Method Handles	
- **JEP 277: Enhanced Deprecation**	
- JEP 285: Spin-Wait Hints	
- JEP 290: Filter Incoming Serialization Data	
- JEP 259: Stack-Walking API	
- JEP 255: Merge Selected Xerces 2.11.0 Updates into JAXP	

+++

#### JEP 254: Compact Strings
[benchmarks](http://cr.openjdk.java.net/~shade/density/state-of-string-density-v1.txt)
[report](http://cr.openjdk.java.net/~huntch/string-density/reports/String-Density-SPARC-jbb2005-Report.pdf)

<ul>
<li class="fragment">**21%** reduction in live data (retained bytes after a GC) (363 MB vs 458 MB)</li>
<li class="fragment">**23%** longer amount of time between in GC events during the heaviest load of benchmark execution, (29 seconds vs 23.5)</li>
<li class="fragment">**12%** lower GC time (430 ms vs 490 ms)</li>
<li class="fragment">**10%** improvement in throughput performance score (37002, 33403)</li>
</ul>

Note:
Looks promising, can be biased though. Time will tell.

In JEP 192: String Deduplication in G1 (JDK 8) some other improvement was added

In terms of memory footprint reduction, the amount of live data during heaviest load of the
benchmark execution, the String Density JDK shows a 21% reduction in live data (retained bytes
after a GC) in the Java heap versus a JDK 9 baseline, (363 MB for String Density, 458 MB for
baseline JDK 9).
In terms of the frequency of GC, the String Density JDK allowed the application to execute
23% longer amount of time between in GC events during the heaviest load of benchmark
execution, (29 seconds for String Density JDK, 23.5 seconds for JDK 9 baseline). Since the
workload is run for a specific amount of wall clock time, the total number of GC events observed
with the String Density is about 17% fewer, (15 for String Density, 18 for baseline JDK 9).
STRING DENSITY 1
Secondarily, in terms of the amount of time spent in GC when under peak load, the String
Density JDK observed about 12% lower GC time than that of the baseline JDK 9, (430 ms for
String Density, 490 ms for baseline JDK 9). And, in terms of the throughput performance score
at peak load, the String Density JDK realized about a 10% improvement in throughput
performance score versus the baseline JDK 9, (37002 for String Density JDK, 33403 for baseline
JDK 9).
Hence, in all metrics observed as goals for the experiment there is an improvement with the
String Density JDK. 

+++

#### JEP 277: Enhanced Deprecation	

```java
@Deprecated(since="9", forRemoval=true)
```

New tool available - `jdeprscan`

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

+++?image=https://media.giphy.com/media/BC3RANWyJtlgA/giphy.gif&size=auto 50%

---

## And remember:
>New is always better!

<span style="font-size:0.6em; color:gray; float:right;">Barney Stinson</span>



