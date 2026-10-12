# Day 1: Technical Interview Questions

## 1. What is asynchronous programming in JavaScript/Node.js?

Asynchronous programming lets an application start an operation that may take time—such as reading a file, making a network request, or querying a database—and continue doing other work instead of waiting for that operation to finish. When the operation completes, its result is handled later. This is especially useful in Node.js, where non-blocking I/O helps a server handle many requests without dedicating a thread to wait on each one.

JavaScript commonly handles asynchronous work with:

- **Callbacks:** functions passed to an operation and called when it completes.
- **Promises:** objects representing a result that will be available later; they can be chained with `.then()` and `.catch()`.
- **`async`/`await`:** syntax built on Promises that makes asynchronous code read more like sequential code.

```javascript
async function loadUser(id) {
  try {
    const response = await fetch(`/api/users/${id}`);
    if (!response.ok) {
      throw new Error(`Request failed: ${response.status}`);
    }
    return await response.json();
  } catch (error) {
    console.error("Could not load user:", error);
    throw error;
  }
}
```

`await` pauses this function until the Promise settles, but it does not block Node.js's event loop from handling other work.

## 2. What is the Virtual DOM in React?

The Virtual DOM is a lightweight, in-memory representation of the UI that React builds from components and their props and state. When data changes, React renders a new representation, compares it with the previous one (a process commonly called **reconciliation**), and applies the necessary updates to the real DOM.

Updating only the affected parts can avoid unnecessary DOM work. The Virtual DOM is an implementation technique; it does not mean every update is automatically faster, and React's reconciliation also uses element identity and keys to determine how lists should be updated.

## 3. What is exception handling in Python?

Exception handling is a way to detect and respond to errors that occur while a program runs, so the program can recover, report a useful message, or clean up resources rather than failing unexpectedly. Python uses `try`, `except`, `else`, and `finally`:

```python
try:
    value = int(user_input)
except ValueError:
    print("Please enter a whole number.")
else:
    print("The number is", value)
finally:
    print("Input processing finished.")
```

- `try` contains code that may raise an exception.
- `except` handles a matching exception. Catch specific exception types rather than using a bare `except`.
- `else` runs if the `try` block completed without an exception.
- `finally` runs whether or not an exception occurred, making it useful for cleanup.

Use `raise` to signal an error or re-raise one when it cannot be handled at the current level.

## 4. What is a REST API, and how does it work?

A REST API is a web API designed around resources and a set of architectural constraints known as Representational State Transfer (REST). A client identifies a resource by its URL and sends an HTTP request to a server. The server processes the request and returns an HTTP status code and, often, a representation of the resource such as JSON.

For example, an API might expose `/users/42`:

- `GET /users/42` retrieves user 42.
- `POST /users` creates a user using the request body.
- `PUT /users/42` replaces user 42, while `PATCH /users/42` changes selected fields.
- `DELETE /users/42` removes user 42.

REST emphasizes a uniform interface, stateless requests (each request contains the information needed to process it), and separation between client and server. APIs commonly use HTTPS, authentication, validation, and status codes such as `200 OK`, `201 Created`, `400 Bad Request`, and `404 Not Found`.

## 5. What is cloud computing? Explain IaaS, PaaS, and SaaS.

Cloud computing provides computing resources—such as servers, storage, databases, and software—over a network, typically on demand. Instead of owning and maintaining all the underlying hardware, customers can provision resources from a provider and often pay based on usage.

The service models differ mainly in how much the provider manages:

- **IaaS (Infrastructure as a Service):** The provider manages physical infrastructure and virtualization; the customer manages operating systems, applications, and data. Examples include virtual machines and cloud networks.
- **PaaS (Platform as a Service):** The provider also manages the operating system and application runtime. The customer focuses on deploying and managing application code and data. Examples include managed application-hosting platforms.
- **SaaS (Software as a Service):** The provider delivers a complete application, usually through a browser or app, and manages the platform and infrastructure. The customer uses the software and configures its available settings. Examples include web-based email and document collaboration tools.

In short: **IaaS gives you infrastructure, PaaS gives you a platform to build and run applications, and SaaS gives you a finished application to use.**