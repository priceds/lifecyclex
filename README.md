<div align="center">

# ⚙️ LifecycleX

### A Modern IoC / Dependency Injection Container for .NET 10  
**Built from scratch to understand lifetimes, scopes, and resolution — deeply.**

<img src="https://readme-typing-svg.herokuapp.com?font=Inter&size=22&duration=2800&pause=900&center=true&vCenter=true&width=700&lines=Dependency+Injection%2C+demystified.;From+first+principles%2C+not+magic.;Learning+systems+by+building+them." />

<br/>

![.NET](https://img.shields.io/badge/.NET-10-512BD4?style=for-the-badge&logo=dotnet&logoColor=white)
![C#](https://img.shields.io/badge/C%23-Modern-239120?style=for-the-badge&logo=csharp&logoColor=white)
![Architecture](https://img.shields.io/badge/Focus-Architecture-black?style=for-the-badge)

</div>

---

## 🧠 What is LifecycleX?

**LifecycleX** is a learning-first, architecture-grade **IoC / Dependency Injection container** implemented in **.NET 10**, designed to explore *how DI actually works* — not just how to use it.

This is not a wrapper.  
This is not a shortcut.  
This is **DI built from first principles**.

---

## 🎯 Why LifecycleX Exists

Most developers *use* dependency injection.  
Fewer can explain:

- how lifetimes are enforced
- how scopes isolate instances
- how constructors are selected
- how disposables are tracked
- why captive dependencies are dangerous

LifecycleX exists to **answer those questions in code**.

---

## ✨ Core Capabilities

### 🔁 Lifetimes (Aligned with .NET DI)
- **Transient** — new instance every resolution
- **Scoped** — one instance per logical scope
- **Singleton** — one instance for container lifetime

### 🧩 Registrations & Resolution
- Constructor injection (greedy strategy)
- Factory delegates (`Func<T>`)
- Instance registrations
- Open generics (`IRepository<T> → Repository<T>`)
- `IEnumerable<T>` resolution
- Circular dependency detection

### 🧼 Scope & Disposal
- Explicit scope creation (`CreateScope`)
- Deterministic disposal of scoped services
- Supports `IDisposable` and `IAsyncDisposable`
- No scope leakage by design

---

## 🚀 Minimal Usage

```csharp
var services = new ServiceCollection();

services.AddSingleton<IClock, SystemClock>();
services.AddScoped<IUserRepository, UserRepository>();
services.AddTransient<UserService>();

using var provider = services.BuildServiceProvider();

using var scope = provider.CreateScope();
var service = scope.ServiceProvider.GetRequiredService<UserService>();
