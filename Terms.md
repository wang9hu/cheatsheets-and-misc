## Web-related terms {#webterms}

- **URI** (Uniform Resource Identifier): a string that refers to a resource
- **URL** (Uniform Rsource Locator): a type of URI, specifies where a resource can be found on the Internet (Web address).
  <br>
- `Host`: a device connected to the Internet (or a local network).

  - clients and servers are just programs that run on a host
    <br>

- **Origin**: `[scheme]://[hostname]:[port]`

  - defined by the scheme (**protocol**), hostname (**domain**), and port of the URL
  - `http://example.com:8080`
    - `http`: called "scheme",
      - http: resources transported over unencrypted connections using HTTP protocol.
      - https: resource is transported using the HTTP protocol, but over a secure TLS (Transport Layer Security) channel.
    - `example.com`: called domain name, it is hosted on a server where the document resides
    - `8080`: called ports
    - `wwww.example.com` is actually a subdomain of `example.com`
  - "Same-origin" means the client has the same origin as the server it's calling
  - "Cross-origin" means the client origin is different than the server it's calling
  - CORS (Cross-Origin Resource Sharing) is a system, consisting of transmitting HTTP headers, that determines whether browsers block frontend JavaScript code from accessing responses for cross-origin requests.
    <br>

- **Client**: Any device that can send request to server, and receive respond from server;
- **Server**: Any device that can receive a request and respond to it. Server could refer to hardware, software, or both.

  - **Hardware**: a web server is a computer that stores web server software and a websites's component files. It connnects to the Internet and supports phy sical data interchange with other devvices connected to the web
  - **Software**: a web server includes several parts that control how web users access hosted files. At a minimum, this is an HTTP server.
    - An HTTP server is software that understands URLs (web addresses) and HTTP (the protocol your browser uses to view webpages).
    - An HTTP server can be accessed through the domain names of the websites it stores, and it delivers the content of these hosted websites to the end user's device.
      <br>
  - **A static web server** (stack): consists of hardware with an HTTP server(software). Static server sends its hosted files as-is to your browser
  - **A dynamic web server**: consists of a static web server plus extra software, most commonly an _**application server**_ and a **_database_**. The application server updates the hosted files before sending content to your browser via the HTTP server.
    <br>
  - **Routing**: determines which handler receives a specific request.

    - A handler is a function dedicated to receiving and acting on certain requests.
    - Requests are routed based on two pieces of information: the HTTP request method, and the request path.
    - A route refers to an HTTP method, path, and handler combination.
    - Routes are created and added to the server before it starts listening for requests.
      <br>

  - **REST**: representational state transfer, a software **architectural** style that describes a uniform interface between physically separate components, often across the Internet in a client-server architecture.
    - RESTful routes:
      <br>

- **Static Media**: refers to content that never or rarely change, like images, movies, audio, etc
  <br>
- **Domain Name System** (DNS): the protocol used to translate **human readable hostnames** into **IP addresses**.
  <br>
- **Streaming** involves breaking a resource that you want to receive over a network down into small chunks, then processing it bit by bit.
  <br>
- **CDN**: content delivery network
  <br>
- **SPA**:single page application
  <br>
- **Idempotency** means that multiple identical requests will have the same outcome
  - Safe methods: HTTP method if it doesn't alter the state of the server.
    - `GET`, `HEAD`, `OPTIONS`.
  - all safe methods are idempotent request, as well as `PUT` and `DELETE`.
    <br>

##### **[Back to table](#table)**

---

**imperative** vs **declarative** programming:

- imperative code focuses on writing an explicit sequence of commands to describe how you want the computer to do things (how to do it)
  ```
  function multiplyByTwo(arr) {
    const result = [];
    for (let i = 0; i < arr.length; i++) {
     result.push(arr[i] * 2);
    }
    return result;
  }
  ```
- declarative code focuses on specifying the result of what you want (what to do)
  - sql queries are mostly declarative: `SELECT * FROM Users WHERE Sex = 'male';`
  - html, css are declarative
  - same code could be reusable
  ```
  function multiplyByTwo(arr) {
   return arr.map((item) => item * 2);
  }
  ```

---
