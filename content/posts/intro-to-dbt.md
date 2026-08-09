---
title: "Intro to dbt"
date: 2026-08-09
type: "posts"
tags:
  - dbt
  - data engineering
  - analytics
summary: "A beginner-friendly introduction to dbt, the analytics engineering framework for transforming data in the warehouse."
---

dbt (data build tool) is a modern analytics engineering framework that helps teams transform data in their warehouse using software engineering best practices.

## What dbt does

- Converts raw data into clean, modeled tables using SQL.
- Enables modular, version-controlled data transformation workflows.
- Automatically generates dependency graphs and documentation.
- Supports testing, documentation, and deployment for analytics code.

## Why dbt matters

Using dbt helps teams:

- keep transformation logic easy to understand,
- collaborate on analytics code,
- reduce errors with tests,
- and maintain reproducible data models.

## Core concepts

- **Models**: SQL files that define transformed tables.
- **Sources**: Definitions for raw tables in the warehouse.
- **Seeds**: Static CSV data loaded into the warehouse.
- **Tests**: Assertions for data quality and schema expectations.
- **Docs**: Auto-generated documentation from model metadata.

## Getting started

1. Install dbt with `pip install dbt-core` or use the adapter package for your warehouse.
2. Initialize a new project with `dbt init my_project`.
3. Add SQL model files under `models/`.
4. Run `dbt run` to build models and `dbt test` to validate them.

## When to use dbt

Use dbt when you want a structured layer of analytics transformations in your warehouse, with clear lineage, version control, and testing support.

---

This guide introduces the basic value and workflow for dbt in analytics engineering.