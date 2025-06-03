---
layout: default
title: "Week 1 Blog: Mastering CVSS 3.1"
hide_navigation: true
---

# Week 1 Blog: Mastering CVSS 3.1 - A Vulnerability Analyst's Deep Dive

*Day 3 of my interview preparation journey*

<a href="{{ '/' | relative_url }}" class="btn-back">← Back to Home</a>

## Why CVSS Matters More Than Ever

As a vulnerability management analyst with 3+ years of Qualys experience, I thought I knew vulnerability scoring. But preparing for my next role made me realize there's always more to learn about CVSS 3.1.

## CVSS 3.1 vs 3.0: What Actually Changed?

The key improvements in CVSS 3.1:

**Environmental Score Refinements:**
- Better handling of partial mitigations
- Clearer guidance on Modified Base metrics
- Improved calculation for defense-in-depth scenarios

**Metric Clarifications:**
- Attack Complexity now better distinguishes automated vs manual attacks
- Scope changes have clearer definitions
- User Interaction guidance is more precise

## Real-World Scoring Examples

### Example 1: SQL Injection in Web Application
**Base Score Calculation:**
- Attack Vector: Network (AV:N) = 0.85
- Attack Complexity: Low (AC:L) = 0.77
- Privileges Required: None (PR:N) = 0.85
- User Interaction: None (UI:N) = 0.85
- Scope: Changed (S:C)
- Confidentiality: High (C:H) = 0.56
- Integrity: High (I:H) = 0.56
- Availability: None (A:N) = 0.00

**Result: CVSS 9.6 (Critical)**

### Example 2: Local Privilege Escalation
**Base Score:** 7.8 (High)
**Environmental Adjustments:**
- Modified Confidentiality: High (business-critical data)
- Modified Availability: Low (redundant systems)
**Environmental Score:** 6.8

## Key Lessons Learned

1. **Context is King** - Environmental scoring is crucial for accurate risk assessment
2. **Scope Changes** - Most impactful metric for determining severity
3. **Temporal Scoring** - Often overlooked but valuable for prioritization

## Tools I'm Using
- [FIRST.org CVSS Calculator](https://www.first.org/cvss/calculator/3.1)
- Custom Excel spreadsheet for batch calculations
- Qualys VMDR integration for automated scoring

## Tomorrow's Focus
Diving into Tenable Nessus fundamentals and comparing scanning methodologies.

---
*Follow my interview prep journey as I expand from Qualys expertise to multi-tool vulnerability management mastery.*

### Related Posts
- [Week 2: Tool Comparison Analysis](week2-tool-comparison)
- [Week 3: Executive Communication](week3-executive-communication)
- [Week 4: Interview Success](week4-interview-success)