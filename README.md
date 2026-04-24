# datamesh

A collection of AI agent skills for **Microsoft Fabric** data engineering, analytics, and real-time intelligence workloads. These skills provide step-by-step guidance and executable patterns for building modern data platforms on Fabric — from raw ingestion to curated analytics.

## Overview

This repository contains reusable skills designed to be invoked from AI coding agents (GitHub Copilot, Claude Code, Cursor, Windsurf, and others). Each skill encapsulates expert knowledge for a specific Fabric capability, covering both **authoring** (creating and managing resources) and **consumption** (querying and analyzing data).

## Available Skills

| Skill | Description |
|-------|-------------|
| **e2e-medallion-architecture** | Implement end-to-end Bronze / Silver / Gold lakehouse patterns using PySpark, Delta Lake, and Fabric Pipelines |
| **spark-authoring-cli** | Develop Fabric Spark notebooks, PySpark applications, data pipelines, and lakehouse infrastructure via CLI |
| **spark-consumption-cli** | Analyse lakehouse data interactively using Fabric Livy sessions, PySpark DataFrames, and Delta time-travel |
| **eventhouse-authoring-cli** | Execute KQL management commands — table creation, ingestion, policies, functions, and materialized views — against Fabric Eventhouse |
| **eventhouse-consumption-cli** | Run read-only KQL queries against Fabric Eventhouse for real-time intelligence and time-series analytics |
| **powerbi-authoring-cli** | Create, manage, and deploy Power BI semantic models inside Fabric workspaces via the Fabric and Power BI REST APIs |
| **powerbi-consumption-cli** | Execute DAX queries and discover semantic model metadata via the Power BI REST API |
| **sqldw-authoring-cli** | Execute authoring T-SQL (DDL, DML, ingestion, stored procedures) against Fabric Data Warehouse and SQL endpoints |
| **sqldw-consumption-cli** | Run read-only T-SQL queries against Fabric Data Warehouse, Lakehouse SQL endpoints, and Mirrored Databases |
| **check-updates** | Check for skill marketplace updates and display the changelog when a new version is available |

## Usage

Skills are loaded automatically by supported AI agents. Invoke a skill by describing your task in natural language — the agent will route to the appropriate skill based on trigger phrases.

**Example triggers:**

- *"set up a medallion architecture with Bronze, Silver, and Gold lakehouses"* → `e2e-medallion-architecture`
- *"create a KQL table and ingest data into Eventhouse"* → `eventhouse-authoring-cli`
- *"run a DAX query against my semantic model"* → `powerbi-consumption-cli`
- *"create a table in the Fabric warehouse"* → `sqldw-authoring-cli`

## Requirements

- A Microsoft Fabric workspace with appropriate capacity
- Azure CLI (`az`) authenticated with the required permissions
- An AI coding agent that supports custom skills (GitHub Copilot, Claude Code, Cursor, Windsurf, Codex, etc.)
