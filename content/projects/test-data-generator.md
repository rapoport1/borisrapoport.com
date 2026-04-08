---
title: Smart Test Data Generator
description: Python utility for generating realistic, contextual test data for document automation and form validation systems.
date: 2024-11-20
status: Active
tech: ["Python", "Faker", "SQLite", "JSON"]
github: "https://github.com/brapoport/test-data-generator"
---

## Smart Test Data Generator

A **Python-based test data generator** that creates realistic, contextually consistent test datasets for document generation and form validation testing.

### Problem Solved

Manual test data creation is tedious, inconsistent, and error-prone. This tool generates **production-realistic data** in seconds, enabling comprehensive test coverage without the tedium.

### Key Features

- **Contextual generation** — Addresses match postal codes, phone numbers follow country conventions
- **Bulk export** — Generate hundreds of test cases in JSON, CSV, or SQL formats
- **Reproducible seeds** — Same seed produces identical datasets for deterministic testing
- **Custom templates** — Define your own data schemas and generation rules
- **Relationship mapping** — Maintains referential integrity across generated records

### Usage

```bash
python generate.py --records 500 --format json --template wes-document
```

### Impact

Reduced test case preparation time from hours to minutes, enabled property-based testing with diverse datasets, and improved edge case coverage for document generation logic.

**Status:** Active and continuously expanded with new templates.
