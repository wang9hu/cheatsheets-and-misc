# Table of contents
- [Table of contents](#table-of-contents)
    - [Web-related terms](#web-related-terms)
    - [Concepts](#concepts)
    - [ASCII vs Unicode (UTF-8, UTF-16 \& UTF-32)](#ascii-vs-unicode-utf-8-utf-16--utf-32)
    - [Elliptic Curve Cryptography (ECC)](#elliptic-curve-cryptography-ecc)

---


### Web-related terms

- <span>URI</span> (Uniform Resource Identifier): a string that refers to a resource
- <span>URL</span> (Uniform Rsource Locator): a type of URI, specifies where a resource can be found on the Internet (Web address).
  <br>
- <span>Host</span>: a device connected to the Internet (or a local network).

  - clients and servers are just programs that run on a host
    <br>

- <span>Origin</span>: `[scheme]://[hostname]:[port]`

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

- <span>Client</span>: Any device that can send request to server, and receive respond from server;
- <span>Server</span>: Any device that can receive a request and respond to it. Server could refer to hardware, software, or both.

  - <span>Hardware</span>: a web server is a computer that stores web server software and a websites's component files. It connnects to the Internet and supports phy sical data interchange with other devvices connected to the web
  - <span>Software</span>: a web server includes several parts that control how web users access hosted files. At a minimum, this is an HTTP server.
    - An HTTP server is software that understands URLs (web addresses) and HTTP (the protocol your browser uses to view webpages).
    - An HTTP server can be accessed through the domain names of the websites it stores, and it delivers the content of these hosted websites to the end user's device.
      <br>
  - <span>A static web server</span> (stack): consists of hardware with an HTTP server(software). Static server sends its hosted files as-is to your browser
  - <span>A dynamic web server</span>: consists of a static web server plus extra software, most commonly an _**application server**_ and a **_database_**. The application server updates the hosted files before sending content to your browser via the HTTP server.
    <br>
  - <span>Routing</span>: determines which handler receives a specific request.

    - A handler is a function dedicated to receiving and acting on certain requests.
    - Requests are routed based on two pieces of information: the HTTP request method, and the request path.
    - A route refers to an HTTP method, path, and handler combination.
    - Routes are created and added to the server before it starts listening for requests.
      <br>

  - <span>REST</span>: representational state transfer, a software **architectural** style that describes a uniform interface between physically separate components, often across the Internet in a client-server architecture.
    - RESTful routes:
      <br>

- <span>Static Media</span>: refers to content that never or rarely change, like images, movies, audio, etc
  <br>
- <span>Domain Name System</span> (DNS): the protocol used to translate **human readable hostnames** into **IP addresses**.
  <br>
- <span>Streaming</span> involves breaking a resource that you want to receive over a network down into small chunks, then processing it bit by bit.
  <br>
- <span>CDN</span>: content delivery network
  <br>
- <span>SPA</span>:single page application
  <br>
- <span>Idempotency</span> means that multiple identical requests will have the same outcome
  - Safe methods: HTTP method if it doesn't alter the state of the server.
    - `GET`, `HEAD`, `OPTIONS`.
  - All safe methods are idempotent request, but not all idempotent methods are safe. 
    - For example, `PUT` and `DELETE` are idempotent, but not safe.
    <br>

- <span>cookies</span> vs <span>localStorage</span> vs <span>sessionStorage</span>
  - **cookies**: used for persist data of certain domain, primarily set and read by server-side(when receiving/sending requests)
    - usually have a limit size of 4KB per domain, some browsers, like chrome, don't have size limit
  <br>
  - **localStorage**: used for persist data of certain domain, primarily be read by client-side
    - Have a limit size of 10MB per domain
    - `localStorage.setItem(key, value)`: adding a data item
    - `localStorage.getItem(key)`: reading a data item
    - `localStorage.removeItem(key)`: removing a data item
    - `localStorage.clear()`: removing all data items
    <br>
  - **sessionStorage**: same as `localStorage`, except that sessionStorage will get cleared when page is closed.
    <br>

- <span>HTTP</span>, <span>HTTPS</span>, <span>SSL</span>, <span>TLS</span>
  - HTTP: Hypertext Transfer Protocol
  - HTTPS: Secure Hypertext Transfer Protocol
  - SSL: Secure Socekt Layer
    - SSL certificate: 
  - TLS: Transport Layer Security (latest industry standard)

 **[Back to table](#table-of-contents)**

---

### Concepts

- <span>Imperative</span> vs <span>Declarative</span> programming:

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
    <br>

- <span>Symmetric</span> vs <span>Asymmetric</span> encryption
  - **symmetric**: use a **single** key to encrypt and decrypt data
  - **asymmetric**: uses two keys - one **public** and one **private** - to encrypt and decrypt data

- <span>JWTs (JSON Web Tokens)</span>
  - Three main parts: `[Header].[Payload].[Signature]`
    - Header: consists of token type and hashing algorithm, Base64Url encoded.
      - `{ 'typ': 'JWT', 'alg': 'HS256' }`
    - Payload: actual "claim", like unique identifier, expiration time, issuer..., Base64Url encoded.
      - `{ "sub": "1234567", "name": "John Doe", "iat": 14225354532 ...}`
    - Signature: hashing header and payload together with a secret key. The primary goal of the signature is to ensure that the message has not been altered during transfer.
---

### ASCII vs Unicode (UTF-8, UTF-16 & UTF-32)
- **encoding**: assigning numbers (code point) to graphical characters (*grapheme*)
<br>

- **ASCII**: a character encoding mapping table: bits(0s and 1s) -> character
  - 1 byte: 
    - 7 bits for encoding, 2^7 = 128 (0 - 127) characters; 
    - 1 bit as Parity bit for error checking: 
    - 65(decimal) -> 1000001(binary) -> A
  - Drawbacks: 
    - only number, English alphabet and punctuations
<br>
- **Unicode**: universal character encoding
  - support many languages and even emojis
  - only an abstract representation of the text, need to encoding
<br>
- **UTF**: Unicode transformation format
  - encoding strategies: UTF-8, UTF-32, ....
    - UTF-8: requires 8, 16, 24 or 32 bits (one to four bytes) to encode a Unicode character, unequal size in bytes for each character, save spaces
    - UTF-16: requires either 16 or 32 bits to encode a character
    - UTF-32: always requires 32 bits to encode a character
    <br>
  - must use the **same strategy** for decode

### Elliptic Curve Cryptography (ECC)
  - a public key crypto system, a type of cryptography
  - Trapdoor function: 
    - A -> B easy while B -> A very difficult
    - e.g. RSA
  - ECC vs RSA
    - same level of sercuirty: 
      - 256 bits (better) vs 3072 bits
      - Top secret level: 384 bits vs 7680 bits
  - 