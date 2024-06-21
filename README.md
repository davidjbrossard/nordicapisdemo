# Nordic APIs Demo
A repository containing all the artifacts necessary for the Nordic APIs demo

# Introduction

At The Nordic APIs Summit, Jonas Iggbom and David Brossard will secure an API live in front of the audience. We will start from scratch with a basic API (records) and add in an API gateway, OAuth AS, and ABAC Authorization Service.

```mermaid
sequenceDiagram
    participant User
    participant API Gateway
    participant Backend API
    User->>API Gateway: HTTP GET /records/123
    API Gateway->>Curity: Validate Access Token
    Curity-->>API Gateway: Token is valid. The user is Alice
    API Gateway->>Axiomatics: Can User Alice get access to record 123?
    Axiomatics-->>API Gateway: Access Permitted
    API Gateway->>Backend API: HTTP GET /records/123
    Backend API-->>API Gateway: record 123
    API Gateway->>Axiomatics: Can Alice get access to section a, b, c of record 123??
    Axiomatics-->>API Gateway: Permit, Deny, Permit.
    API Gateway->>API Gateway: Redact section b
    API Gateway-->>User: redacted record 123

```

# Running Instructions

````
docker compose pull
docker compose build
docker compose up
````

Note that docker compose build may have auth errors when pulling images. This will require you to manually docker pull those images and then rerun docker compose build.