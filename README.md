<div align="center">

# ⚙️ LifecycleX
### High-Fidelity IoC Container & Dependency Injection System

<img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&size=22&duration=3000&pause=1000&center=true&vCenter=true&width=700&lines=Zero+Magic.+Pure+Architecture.;Implemented+in+.NET+10.;From+First+Principles." />

<br/>

[![.NET 10](https://img.shields.io/badge/.NET%2010-512BD4?style=for-the-badge&logo=dotnet&logoColor=white)](https://dotnet.microsoft.com/)
[![Architecture](https://img.shields.io/badge/Pattern-Inversion_of_Control-black?style=for-the-badge&logo=uml&logoColor=white)](https://martinfowler.com/articles/injection.html)
[![License](https://img.shields.io/badge/License-MIT-blue?style=for-the-badge)](LICENSE)

<br/>

> **"You don't truly understand an abstraction until you can rebuild it from scratch."**

</div>

---

## 🏛️ System Design Philosophy

**LifecycleX** is not just another wrapper. It is an architectural study in **Life-cycle Management** and **Object Graph Resolution**, built on the bleeding edge of **.NET 10**.

While most developers consume Dependency Injection (DI) as a black box, LifecycleX peers inside to solve the hard problems:
1.  **Memory Management:** Preventing scope leakage and ensuring deterministic disposal.
2.  **Graph Theory:** Resolving complex dependency chains (DAGs) and detecting circular references.
3.  **Reflection & Performance:** Efficient constructor selection strategies.

---


## 🏗️ Architecture Overview

LifecycleX implements the core Container/Provider pattern using a strictly decoupled architecture. The system treats dependencies as a **Directed Acyclic Graph (DAG)**, managing resolution depth and strictly enforcing lifetime boundaries.

```text
  REGISTRATION PHASE                     RESOLUTION PHASE
  ┌─────────────────┐                  ┌──────────────────┐
  │ ServiceCollection │                  │  Client Request  │
  └────────┬────────┘                  └─────────┬────────┘
           │ Register                            │ GetRequiredService
           ▼                                     ▼
  ┌─────────────────┐                  ┌──────────────────┐
  │ ServiceRegistry │ <─────────────── │ ServiceProvider  │
  └─────────────────┘      Lookup      └─────────┬────────┘
                                                 │
                                       ┌─────────┴─────────┐
                                       ▼                   ▼
                            ┌──────────────────┐   ┌────────────────┐
                            │ Lifetime Manager │   │ Constructor    │
                            └────────┬─────────┘   │    Injector    │
                                     │             └───────┬────────┘
                  ┌──────────────────┼──────────────────┐  │
                  ▼                  ▼                  ▼  ▼
          ┌──────────────┐   ┌──────────────┐    ┌────────────┐
          │   Scoped     │   │  Singleton   │    │ Transient  │
          │    Cache     │   │    Cache     │    │ (No Cache) │
          └──────────────┘   └──────────────┘    └────────────┘
          
