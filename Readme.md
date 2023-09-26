# `Specular`

## 😅 What is this?

Specular is an open-source toolkit designed for constructing Web APIs, accompanied by effortlessly generated Client SDKs across multiple programming languages and platforms. These SDKs are so seamless, they feel **hand-written**.

The toolkit boasts a user-friendly API DSL, alongside Compiler and Runtime libraries.

## 🧐 Why are you building this?

We're crafting a platform tailored for developers, and we developers have a soft spot for client SDKs.

## 🥺 Why not use something that already exists?

We have 20+ years of experience as developers, we've tried everything:

### REST

* Its specification feels like an afterthought, not tailored for client SDKs that feel hand-written.
* It lacks streaming support.

### GRPC
* It lacks sufficient metadata to generate user-friendly native errors/exceptions.
* Generated type names can be messy and with excessive stuttering
* While it excels in server-to-server communication or IPC, it's less optimized for the web. We're aiming for a solution that's more browser-friendly.

### GraphQL

* It's ideal for front-end developers but falls short for others.
* Generated type names can be messy, much worse than GRPC
* There's insufficient metadata to generate intuitive native errors/exceptions
* It offers excessive query flexibility for our taste.
* While the specification supports streaming, most clients are limited to WebSocket transport. Its 2023, we rather use HTTP2+.
* We don't love the separation of input types vs types output

## 📚 Inspirations?

The DSL syntax draws significant influences from Smithy, GraphQL, and GRPC.

As for the runtime, it's deeply rooted in the principles of GRPC and the Go Open-API runtimes.

## 🥸 How does it work?

Start by defining your RPC operations in a singular specular file. The specular compiler then generates server stubs for your implementation. Using that same specification, it also crafts client SDKs tailored for various programming languages and platforms.

Here's a sample `package.specular` file:

```ruby
package Deployport/SpecularExamples/CRMExample

# CRM Contact
struct Contact {
    id: string!
    firstName: string!
    lastName: string!
}

resource Contacts {
    # Creates a new contact
    operation Create {
        input struct {
            contact: Contact!
        }
        output struct {
            contact: Contact!
        }

        # occurs when the contact name is not valid
        raises struct InvalidContactName {}
    }

    streamed operation Watch {
        input struct {
            # list of contacts to watch
            contactIdentifiers: [string]!
        }
        output struct {
            # changed contact
            contact: Contact!
        }
    }
}
```

## 🤯 What I get?

1. Strongly-typed server-side stubs in Go, ready for your operational implementations.
2. A Go client library that feels as though it's hand-crafted, complete with full typing and documentation.
3. Client SDKs in both JS and Typescript, compatible with both Browser and Node environments.

## 🧢 What programming languages will it support?

We aim to implement generators for all of programming languages:

* Go
* Typescript
* Javascript
* Python
* Ruby
* PHP
* .NET
* Java
* Objective-C
* Swift
* Rust

See our [Language Priority Poll](https://github.com/deployport/specular/issues/1)

## 🏁 What's the status?

We've successfully developed a functioning compiler, as well as generators for both Go server and client (and the client generator's output is truly a thing of beauty ✨).

Our efforts are now directed towards the JS/TS generator.

Once we finalize a stable DSL, we'll roll out v0.1.0.

## 💪🏼 When can I expect to try it?

By the end of 2023.

