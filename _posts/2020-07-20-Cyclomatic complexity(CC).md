---
layout: post
title: Cyclomatic complexity(CC)
date: 2020-07-20
category: category
---

# Cyclomatic complexity(CC)

* A metric used to indicates programs' complexity. Lowere CC code is easy to understand and test. 
* Nodes(N), edges (E) and exit point (EP) in a flow chart for a given piece of code helps to find the CC.

```
CC = E - N + 2*p
```

* CC of range 0-10 is considered an acceptable range. >10 is a complex functionality.
* If a CC of a class is too high, the enclosed methods CC is high. The class may have to be refactored since it may not be following the SRP.
* Breaking the functionality to smaller methods and reducing the if/else checks in the code.

### Tools to help in static code analysis
* PMD ([PMD CC Rules description](https://pmd.github.io/pmd-6.26.0/pmd_rules_java_design.html#cyclomaticcomplexity)) and SonarLint (does more than finding CC)

