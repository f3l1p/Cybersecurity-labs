# 🌐 Exercise – Domain Impersonation Using Homoglyph Attacks (evilURL)

**Author:** Carlos Felipe Chicangana  
**Focus:** Domain impersonation and homoglyph-based phishing  
**Environment:** Local analysis (Python tooling)  

---

## 1️⃣ Introduction

The objective of this exercise was to **generate homoglyph domain names** in order to simulate **domain impersonation attacks**, commonly used in phishing campaigns. The original approach was based on the tool **evilURL**, initially developed by *undeadSec*.

However, during the execution of the exercise, it was identified that **evilURL depends on Python 2**, which is now deprecated and incompatible with modern environments. This limitation caused multiple dependency and execution issues, preventing its proper usage.

As a result, the scope of the exercise evolved to include the **analysis of alternative approaches** and the **development of a custom solution compatible with Python 3**.

---

## 2️⃣ Scope

The main objective was to generate **visually similar variants of a legitimate domain** in order to evaluate phishing techniques based on **homoglyph attacks**.

Due to technical limitations of existing tools, a **custom local Python 3 script** was designed and implemented. This script generates domain names using Unicode characters that visually resemble standard ASCII characters, enabling:

- Security testing  
- Awareness and training exercises  
- Academic and practical demonstrations  

No real domains were registered or used in live environments.

---

## 3️⃣ Methodology

### 3.1 Initial Tool Analysis (evilURL)

1. The following repository was cloned:
