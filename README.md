# Stock Data Extraction – UiPath Automation

## Business Context

Business users and financial analysts often require **up-to-date stock market data** for a predefined list of companies in order to support reporting, analysis, and decision-making. Manually searching for stock prices on the London Stock Exchange website is time-consuming, repetitive, and prone to errors, especially when the number of monitored instruments increases or when the task must be performed on a recurring basis.

From my perspective, the business problem is not limited to a one-time retrieval of stock prices, but rather to providing a **repeatable, scalable, and predictable mechanism for acquiring market data**, which can be safely executed in the background without user supervision.

---

## Solution Overview

The automation was designed primarily as an **unattended solution**, intended to operate in a **cloud-based environment**. It can be executed centrally via UiPath Orchestrator, allowing the process to run without direct involvement of the end user.

The main design goal of the robot is **reliability and fast transaction processing**. For this reason, the solution does **not implement retry mechanisms at the business logic level**. Each transaction is processed exactly once, and any issues encountered are clearly classified as either business or technical errors. This approach ensures a predictable execution time and full control over the quality and consistency of the resulting data.

---

## Input Data Handling

Currently, the robot uses **UiPath Orchestrator Storage Buckets** as the mechanism for delivering input data. This enables:

- centralized management of batch input files,
- execution in a cloud environment,
- no dependency on local file paths on the end-user machine.

---

## Flexibility and Extensibility

Although the solution is designed for unattended cloud execution, its architecture is intentionally **flexible** and allows for quick adaptation to other operating modes.

By extending the `Switch / Case` logic in the Dispatcher, the solution can be easily adjusted to:

- process data from a **local file system path** on the end-user machine,
- receive input data from an **external endpoint** using HTTP requests (e.g. REST API).

This makes the automation suitable both as a **production-grade cloud automation** and as a **lightweight local or integration-oriented robot**, depending on business and environmental requirements.

---

## Key Benefits

- Unattended, cloud-ready execution  
- Predictable and fast batch processing  
- Clear separation of business and technical errors  
- Centralized input management  
- Easy adaptation to local or API-based integrations  

---

## Execution Modes

- **UiPath Orchestrator** – scheduled or centrally triggered unattended execution  
- **UiPath Assistant** – manual, ad-hoc execution for local or testing scenarios  

---

## UiPath Studio Specification

The automation was developed using **UiPath Studio** with the **REFramework** architecture to ensure consistency, maintainability, and robustness of execution.

### Development Environment

- **UiPath Studio:** StudioX / Studio (Cloud-compatible version)
- **Framework:** REFramework
- **Execution Type:** Unattended (primary), Attended (optional via UiPath Assistant)
- **Target Runtime:** UiPath Robot / Cloud Robot
- **Browser Automation:** Modern UI Automation (Edge)

### Architectural Components

- **Dispatcher**
  - Responsible for preparing and distributing workload
  - Reads input data and creates Queue Items
  - Supports multiple input sources via configurable logic (Switch / Case)

- **Performer**
  - Processes individual Queue Items
  - Retrieves stock data from the London Stock Exchange website
  - Aggregates and persists results

### Orchestrator Integration

- **Queues**  
  Used for scalable and independent transaction processing

- **Storage Buckets**  
  Used for centralized input and output file management

- **Assets / Config.xlsx**  
  All environment-specific values are externalized and configurable

### Design Principles

- Configuration-driven execution  
- Stateless transaction processing  
- Clear separation of responsibilities  
- Deterministic cleanup of resources  
- Cloud-ready and environment-agnostic design

---

This setup ensures that the solution can be reliably deployed, monitored, and scaled in both cloud and local execution scenarios.


## Summary

The solution provides a robust and scalable way to automate the acquisition of stock market data, eliminating manual effort while ensuring consistency, reliability, and adaptability to different execution environments.
