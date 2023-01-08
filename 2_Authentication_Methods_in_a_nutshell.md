![cover image of Authentication Methods in a nutshell](https://blog.denilgabani.com/_next/image?url=https%3A%2F%2Fcdn.hashnode.com%2Fres%2Fhashnode%2Fimage%2Fupload%2Fv1673182765493%2F01fb2d52-fee4-403f-ab70-28647fc0f475.jpeg%3Fw%3D1600%26h%3D840%26fit%3Dcrop%26crop%3Dentropy%26auto%3Dcompress%2Cformat%26format%3Dwebp&w=1920&q=75)

# Authentication Methods in a nutshell

In technical or non-technical you must have come across the word Authentication. Here we will go through it from a technical perspective.

### **What is Authentication?**

Authentication is the process of verifying that someone is who they claim to be.

### **Why do we require Authentication?**

It is a crucial security measure that is used to protect against unauthorized access to systems, networks, and data.

Many different methods of authentication can be used, including:

- **Something the user knows:** This could be a password, PIN, or a secret answer to a security question.
- **Something the user has:** This could be a physical token, such as a key or a smart card, or a digital token, such as a one-time password sent via SMS or email.
- **Something the user is:** This could be biometric data, such as a fingerprint or a facial recognition scan.
- **Somewhere the user is**: This could be determined by the user's IP address or GPS location.
- **Something the user does:** This could be a behavioral characteristic, such as the way the user types or swipes on a device.

From various authentication methods users are mostly using password-based user authentication.

Have you ever got a question about how does authentication methods work behind the scene?

Let's go through the common authentication methods that are being used.

![letsgo](https://cdn.hashnode.com/res/hashnode/image/upload/v1673030367040/5fd418ee-a577-48df-9f95-3d78e73f778f.webp)

### **1\. Basic Authentication**

Don’t confuse Basic Authentication with a standard username and password authentication.

Basic authentication is a part of the HTTP specification [RFC7617](https://www.rfc-editor.org/rfc/rfc7617.html).

As it is a part of the HTTP specifications, all the browsers support "HTTP Basic Authentication” Natively.

![credspopup](https://cdn.hashnode.com/res/hashnode/image/upload/v1673029899664/4dd35d76-5985-4abb-bf4e-e87619b593f3.webp)

<center>
Image Source: https://roadmap.sh/guides/http-basic-authentication/
</center>

**How does it work?**

1. Browsers sent requests to the server.
2. Server checks for the Authorization header in the request.
3. If no “**Authorization**” header is found in the request, then the server sends a response with **401 Unauthorized** status code and sends **WWW-Authenticate** header with the value set to **Basic**.
4. **Basic** value tells the browser to trigger the basic authentication flow.
5. Browser then will show an authentication popup.
6. After submitting credentials in the authentication popup browser will encode credentials into **base64** and send them in **Authorization** header.
7. The server will decode and verify this credential. If the credential is valid then it will send the response to the client

**Should we use Basic Authentication?**

1. We should not use it as it is a simple form of authentication that is transmitted in plain text over HTTP.
2. It is susceptible to eavesdropping.
3. It does not provide encryption.
4. It is vulnerable to replay attacks.

### **2\. Session-based authentication (Cookie-based authentication)**

One problem with the above Basic Authentication is that User needs to provide credentials whenever they visit a particular service.

The reason is that request is being made over HTTP which is a stateless protocol.

So to solve this issue Session-based or Cookie-based authentication can be used. It makes authentication stateful.

Meaning authentication records are being kept by both the server and client side.

The server needs to keep track of session memory or database while a cookie is created over the Client side that holds this session identifier.

**How does it work?**

Best auth flow is explained in the below guide by roadmap.sh: [https://roadmap.sh/guides/session-authentication/](https://roadmap.sh/guides/session-authentication/)

Challenges with Session-based Authentication:

1. **Overhead to server:** Every time user authenticates server needs to create a new record and stored it in memory or a database.
2. **Scalability:** As the session is stored in memory it’s problem with scalability as have to replicate all sessions to all multiple instances
3. **Session IDs can be compromised:** If an attacker can obtain a user's session ID, they may be able to gain unauthorized access to the user's account. This can occur through techniques such as session hijacking or session fixation.

### **3\. Token-Based Authentication**

Token-based authentication is a method of authenticating users in which the user provides a username and password, and in return, the server sends a token.

The user then sends this token with each subsequent request, allowing the server to verify the user's identity without requiring the user to provide their password again.

**Make sure to visit this to know how token-based authentication works:** [https://roadmap.sh/guides/token-authentication/](https://roadmap.sh/guides/token-authentication/)

**Few examples of Token Based Authentication strategies:**

1. JSON Web Token (JWT)
2. OAuth
3. SAML (Security Assertion Markup Language)
4. OpenID Connect
5. Two-Factor Authentication (2FA)

We will go through most of these strategies one by one so stay tuned.

**Advantages of Token-Based Authentication:**

1. Stateless: It’s completely stateless so the server doesn’t need to store any record of the user token/sessions
2. Scalable: Because the server does not need to verify the user's password with each request, token-based authentication can be more scalable than session-based authentication.
3. Store any type of metadata: Tokens can store metadata. For example, a JWT payload might contain The user's name, email address, role or permissions within the application, the time the token was issued, the duration of time the token is valid, and many other things.

### **4\. JWT (JSON Web Token)**

If you have ever implemented an authentication mechanism in your web or app then you have come across JWT for sure.

JWT is a form of Token Based Authentication.

To know step-by-step flow on how JWT authentication works make sure to visit this guide: [https://roadmap.sh/guides/jwt-authentication/](https://roadmap.sh/guides/jwt-authentication/)

**Pros:**

- JWTs are self-contained: Because the claims are contained within the token itself, JWTs do not require a separate store of data (such as a database) to validate the claims. This can make them easier to use and more scalable.
- JWTs are stateless: Because the server does not need to maintain a session or other state information, JWTs can be simpler to implement and more scalable than other methods of authentication that require server-side state.
- JWTs can be signed: JWTs can be signed using a secret or public/private key pair, which allows the server to verify the authenticity of the token. This can help to prevent tampering and spoofing.

**Cons:**

- JWTs can be large: Because the claims are contained within the token itself, JWTs can become quite large, especially if there is a lot of metadata being stored within the token. This can be an issue if the token needs to be transmitted over a network or stored in a cookie.
- JWTs cannot be easily revoked: Because JWTs are self-contained, it can be difficult to revoke a token once it has been issued. This can be an issue if a user's permissions change or if the user's account is compromised.
- JWTs can be vulnerable to attacks: If an attacker is able to obtain a JWT, they may be able to gain unauthorized access to protected resources. This can be an issue if the JWT is not properly signed or if the secret used to sign the JWT is compromised.

### **5\. SAML 2.0 (Security Assertion Markup Language)**

SAML (Security Assertion Markup Language) is a standard protocol used for securely exchanging authentication and authorization data between parties.

It is often used to enable single sign-on (SSO) for users accessing different systems or applications.

SAML solves a very critical problem which is if a user wants to access more than one service with different backend systems then the user is required to authenticate all these services respectively.

SAML solves this problem by introducing a central service for authentication only.

**Two Most Important terms in SAML:**

1. **IdP (Identity Provider):** Entity providing the identities including the ability to authenticate users.
2. **SP (Service Provider):** Entity Providing the service typically in form of an application.

To know more about other SAML terms and in-depth explanations check this video:

[![SAML Term video](https://img.youtube.com/vi/l-6QSEqDJPo/0.jpg)](https://www.youtube.com/watch?v=l-6QSEqDJPoE)

There are two ways of authentication flow in SAML based on where user starts the flow:

1. **IdP Initiated Sign-in flow:** User first goes to IdP portal and SAML sigin-in flow starts from IdP side.

   ![IdPinitiatedflow](https://cdn.hashnode.com/res/hashnode/image/upload/v1673029763472/16106d90-5b94-4062-8061-8a27c1c6e2d9.webp)

   Diagram Source: https://www.youtube.com/watch?v=\_P73fndPCbU

2. **SP Initiated Sign-in flow:** User first visits a particular service and to authenticate the user that service redirects to IdP.

   ![spinitiatedflow](https://cdn.hashnode.com/res/hashnode/image/upload/v1673029777070/e472ab05-15ee-43df-90f5-abf1247780cd.webp)

   Diagram Source: https://www.youtube.com/watch?v=Y5J3r1cmHWc

**Advantages of SAML:**

1. Single sign-on: SAML enables users to log in once and access multiple systems and applications without having to re-enter their credentials. This can make it more convenient for users and reduce the risk of password-related security breaches.
2. Wide support: SAML is supported by many different types of software, including web-based applications, mobile apps, and cloud-based services. This makes it easy to integrate SAML into a wide range of systems and environments.
3. Flexibility: SAML allows for a wide range of authentication and authorization scenarios, including the ability to pass information about the user's role and group membership along with the authentication request.
4. Security: SAML uses digital signatures and encryption to secure the authentication and authorization data that is exchanged between parties.

**Disadvantages:**

1. Complexity: SAML can be complex to implement, especially for organizations that are new to the standard.
2. Limited customization: SAML is a standard protocol, which means that it has a fixed set of rules and capabilities. This can make it difficult to customize or extend the protocol to meet the specific needs of an organization.
3. Compatibility issues: SAML relies on a number of different technologies, including XML, digital certificates, and security tokens. This can create compatibility issues if the systems and applications being used do not support these technologies.
4. Integration challenges: SAML requires integration with both the IdP (identity provider) and the SP (service provider), which can be a challenge for organizations that are using a mix of different systems and applications. In order to use SAML, these systems and applications must be able to communicate with each other using the SAML protocol, which can require significant effort and resources.
5. Performance: In some cases, using SAML for authentication and authorization may result in a slight performance hit, as there is additional overhead involved in generating and verifying SAML assertions. This may be particularly noticeable in environments with a large number of users and/or high levels of authentication traffic.

### **6\. OAuth 2.0**

The first thing that needs to clarify about OAuth 2.0 is that Auth in OAuth 2.0 stands for Authorization, not Authentication.

Anyone who has a smartphone they have used OAuth directly or indirectly.

One of the most common examples of OAuth 2.0 in action is when a user grants a third-party application or service access to their social media account (such as their Facebook or Twitter account).

For example, let's say that you want to use a new photo editing app that requires access to your Facebook photos. The app will ask you to log in to your Facebook account and grant it access to your photos. When you do this, the app is using OAuth 2.0 to securely request access to your photos without requiring you to share your Facebook login credentials.

OAuth 2.0 basically used for delegating the Authorization.

To know about OAuth 2.0 and OpenID Connect in plain English checkout below video by Okta Dev:

[![OAuth 2.0 and OpenID Connect in plain English checkout below video by Okta Dev](https://img.youtube.com/vi/996OiexHze0/0.jpg)](https://www.youtube.com/watch?v=996OiexHze0)

**OAuth 2.0 Authorization flow:**

![OAuth2.0authflow](https://cdn.hashnode.com/res/hashnode/image/upload/v1673029808846/a199d393-9bb3-4301-85f5-7240b47f0a2e.webp)

<center>
Diagram Source: https://www.youtube.com/watch?v=996OiexHze0
</center>

**Main Advantages of Using OAuth 2.0:**

1. Improved security: OAuth 2.0 allows users to grant access to their resources without revealing their login credentials, which helps to reduce the risk of password-related security breaches.
2. Ease of use: OAuth 2.0 is designed to be easy for users to understand and use. It allows users to grant access to their resources with just a few clicks, rather than requiring them to enter their login credentials every time they want to access a new service or application.
3. Wide support: OAuth 2.0 is supported by many popular websites and services, including Facebook, Google, Twitter, and Microsoft. It is also supported by a wide range of software libraries and tools, making it easy to integrate into a variety of systems and environments.

**Potential disadvantages of using OAuth 2.0:**

1. Complexity: OAuth 2.0 can be complex to implement, especially for organizations that are new to the standard.
2. Limited customization: OAuth 2.0 is a standard protocol, which means that it has a fixed set of rules and capabilities. This can make it difficult to customize or extend the protocol to meet the specific needs of an organization.
3. Compatibility issues: OAuth 2.0 relies on a number of different technologies, including HTTP, JSON, and SSL/TLS. This can create compatibility issues if the systems and applications being used do not support these technologies.
4. Integration challenges: OAuth 2.0 requires integration with both the resource server (where the user's resources are stored) and the client (the third-party application or service that is requesting access to the resources). This can be a challenge for organizations that are using a mix of different systems and applications.

### **7\. OpenID Connect (OIDC)**

Initially when OAuth was introduced the main issue was developers started to use OAuth for Authentication purposes by implementing their own custom wrapper and which was not the right way as OAuth standard was introduced for Authorization purposes.

So for authentication purposes and with the same working mechanism as OAuth Standard OpenID Connect was introduced.

It provides a standard way for users to authenticate themselves across different websites and applications, without the need to create separate accounts for each one.

OpenID Connect (OIDC) is a simple identity layer built on top of the OAuth 2.0 protocol.

**OpenID Connect Flow:**

![OpenIDConnectflow](https://cdn.hashnode.com/res/hashnode/image/upload/v1673029821906/d61de1e9-5652-4c18-b896-b7fece5acc58.webp)

<center>
Diagram Source: https://www.youtube.com/watch?v=996OiexHze0
</center>

**Advantages of using OIDC:**

1. Single sign-on: OIDC enables users to log in once and access multiple websites and applications without having to re-enter their credentials. This can make it more convenient for users and reduce the risk of password-related security breaches.
2. Wide support: OIDC is supported by many popular websites and services, including Google, Microsoft, and Facebook. It is also supported by a wide range of software libraries and tools, making it easy to integrate into a variety of systems and environments.
3. Flexibility: OIDC allows for a wide range of authentication and authorization scenarios, including the ability to pass information about the user's role and group membership along with the authentication request.
4. Security: OIDC uses digital signatures and encryption to secure the authentication and authorization data that is exchanged between parties.

**Disadvantages of using OIDC:**

1. Complexity: OIDC can be complex to implement, especially for organizations that are new to the standard.
2. Limited customization: OIDC is a standard protocol, which means that it has a fixed set of rules and capabilities. This can make it difficult to customize or extend the protocol to meet the specific needs of an organization.
3. Compatibility issues: OIDC relies on a number of different technologies, including HTTP, JSON, and SSL/TLS. This can create compatibility issues if the systems and applications being used do not support these technologies.
4. Integration challenges: OIDC requires integration with both the identity provider (IdP) and the client (the website or application that is requesting access to the user's resources). This can be a challenge for organizations that are using a mix of different systems and applications.

So this is it. These are the most common Authentication methods that are being used.

Thanks for reading till the end of the blog. We will meet in the next blog 😃.

**To stay updated and learn together follow me on** [@denilgabani](https://twitter.com/denilgabani)

![seeyousoon](https://cdn.hashnode.com/res/hashnode/image/upload/v1673073545388/510a398c-c62f-49e9-9603-f9eac7973730.webp)
