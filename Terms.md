# Table of contents
- [Table of contents](#table-of-contents)
    - [Web-related terms](#web-related-terms)
    - [cookies vs localStorage vs sessionStorage](#cookies-vs-localstorage-vs-sessionstorage)
    - [HTTP, HTTPS, SSL, TLS](#http-https-ssl-tls)
      - [HTTP (Hypertext Transfer Protocal)](#http-hypertext-transfer-protocal)
    - [Concepts](#concepts)
    - [ASCII vs Unicode (UTF-8, UTF-16 \& UTF-32)](#ascii-vs-unicode-utf-8-utf-16--utf-32)
    - [RSA (Rivest–Shamir–Adleman) cryptosystem](#rsa-rivestshamiradleman-cryptosystem)
    - [Elliptic Curve Cryptography (ECC)](#elliptic-curve-cryptography-ecc)

---


### Web-related terms

- <span>URI</span> (Uniform Resource Identifier): a string that refers to a resource
- <span>URL</span> (Uniform Rsource Locator): a type of URI, specifies where a resource can be found on the Internet (Web address).
  <br>
- <span>Host</span>: a device connected to the Internet (or a local network).

  - clients and servers are just programs that run on a host
    <br>

- <span>Origin</span>: `[scheme]://[hostname]:[port]/[path]`

  - defined by the scheme (**protocol**), hostname (**domain**), and port of the URL
  - `http://example.com:8080/test/`
    - `http`: called "scheme",
      - http: resources transported over unencrypted connections using HTTP protocol.
      - https: resource is transported using the HTTP protocol, but over a secure TLS (Transport Layer Security) channel.
    - `example.com`: called domain name, it is hosted on a server where the document resides
    - `8080`: ports
      - When no port is specified in a URL, the default port for the given protocol is used. Here are the default ports for some common protocols:
        •	*HTTP: Port 80*
        •	*HTTPS: Port 443*
        •	*FTP: Port 21*
        •	*SSH: Port 22*
    - `/test/`: path name
    - `wwww.example.com` is actually a subdomain of `example.com`
  <br>

  - "Same-origin" means the client has the same origin as the server it's calling
  - "Cross-origin" means the client origin is different than the server it's calling
  - CORS (Cross-Origin Resource Sharing) is a system, consisting of transmitting HTTP headers, that determines whether **browsers** block frontend JavaScript code from accessing responses for cross-origin requests.
    - **Browser** decide: pass or fail
      - AJAX ---> browser send request ---> server response ---> browser check cors
        - pass: browser ---> response to AJAX
        - fail: browser show cors error
    <br>

    - <span>request types</span>: simple and preflight
      - **simple**: 
        - `GET` `POST` or `HEAD` method 
        - request header compliant with CORS standards
        - Content-Type can only be 
          - `text/plain` (default)
          - `multippart/form-data` 
          - `application/x-www-form-urlencoded`
      - **preflight**: requests that are **NOT** simple request
    <br>

    - <span>validation rules</span>: 
      - **Simple request**: 
        - browser add `Origin: [current_origin]` in request head (browser behavior, can't be changed)
        - pass: in response: `Access-Control-Allow_Origin: [current_origin] || *`
          - in general, don't use `*`, server can just use `req.get('Origin')` to grap the request origin
        - fail: in response, no `Access-Control-Allow-Origin` or no `[current_origin]`
      - **Preflight request**: 
        - browser won't send the request, instead send a `OPTIONS` method request with
          - `Origin: [current_origin]`
          - `Access-Control-Request-Method: [preflight_request_method]`
          - `Access-Control-Request-Headers: a, b, content-type` (changed req head)
        - pass: in response, must have at least these
          - `Access-Control-Allow_Origin: [current_origin]`
          - `Access-Control-Allow-Methods: [could have multiple values, must contain above]`
          - `Access-Control-Allow-Headers: [could have multiple values, must contain above]`
          - optional allowed period (1 day): `Access-Control-Max-Age: 86400`
    <br>

    - Cross-origin AJAX requst generally don't have cookies with it, so it need to set manually
      - requests:
        - XHR: `xhr.withCredentials = true`
        - Fetch: `fetch(url, { credentials: "include" })`

      - response:
        - `Access-Control-Allow-Credentials: true`
        - can't have: `Access-Control-Allow_Origin: *`
    <br>

    - Cross-origin AJAX client can have basic response headers like
      - `Cache-Control、Content-Language、Content-Type、Expires、Last-Modified、Pragma`
      - Client can't have other headers unless response header have
        - `Access-Control-Expose-Headers: authorization, a, b`

    <br>

  - JSONP: handle cross-origin request before CORS exist (mostly deprecated)
    - browser have less restrictiond on tags
    - can only send get request
  
  <br>

  - Proxy: since cors error only happens in browser, use proxy server could avoid it completely
  
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

**[Back to table](#table-of-contents)**

---

### cookies vs localStorage vs sessionStorage
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

**[Back to table](#table-of-contents)**

---

### HTTP, HTTPS, SSL, TLS
  - HTTP: Hypertext Transfer Protocol
  - HTTPS: Secure Hypertext Transfer Protocol
  - SSL: Secure Socekt Layer
    - SSL certificate: 
  - TLS: Transport Layer Security (latest industry standard)
  
  <span>How a packet sent over internet</span>
  - Application Layers:
    - **HTTP**, **FTP**, **DNS**, **SMTP**, **POP3** ...
    - e.g., A web browser requests a webpage using the HTTP protocol
  - Transport Layer:
    - **TCP**, **UDP**
    - e.g., The HTTP request is encapsulated in a TCP segment. This segment includes source and destination port numbers and a sequence number.
  - Network Layer
    - **IP**
    - e.g., The TCP segment is encapsulated in an IP packet, which includes the source and destination IP addresses.
  - Data Link Layer
    - **Ethernet**, **Wi-Fi** ...
    - e.g., The IP packet is encapsulated in an Ethernet frame, which includes source and destination MAC (Media Access Control) addresses.
  - Physical Layer
    - **cable**, **fiber optics**, **wireless**
  - Transmission Across the Network
    - **switches**, **routers**, **modems**
  - Intermediate Hops
    - **multiple routers**
  - Reassembly and Delivery
  

  <span>Diagram of Encapusulation</span>
```
  +----------+-------------------------------------+----------------+
  | Protocal | Encapsulation                       |  Max Seg size  |
  -----------+-------------------------------------+----------------+
  |    App   | Application Data                    |       N/A      |
  +----------+-------------------------------------+----------------+
  |    TCP   | TCP Header + TCP Segment (Data)     |  1440 ~ 1460 B |
  +----------+-------------------------------------+----------------+
  |    IP    | IP Header + IP Packet (TCP Segment) |   ~ 65,535 B   |
  +----------+-------------------------------------+----------------+
  +----------------+-------------------------------+----------------+
  | Ethernet Frame | Ethernet Header + IP Packet   |    ~ 1,500 B   |
  +----------------+-------------------------------+----------------+
  |            Ethernet Frame defines the overall MTU               |
  +-----------------------------------------------------------------+
  Note: maximum transmission unit (MTU)
```

#### HTTP (Hypertext Transfer Protocal)
- Request-response communication
- text based format, only knows ASCII encoding
  - use `encodeURIComponent()` to get the ASCII code for non-ASCII characters
  - use `decodeURIComponent()` to show the non-ASCII character from encoded ASCII
- request has 3 parts:
  - req line, e.g. GET /api/movies?p=2&size=10 HTTP/1.1
    - *GET*: semantic method name, can be customized (if server knows it)
    - /api/movies?p=2&size=10: path
    - HTTP/1.1: http version
  - req head: key-value pairs
    - Host: www.example.com   // domain (**required**)
    - Content-Type: [**type/subtype**]    // req body format
      - `application/x-www-form-urlencoded`   // 'name=John+Doe&age=28&city=New+York' / 'pic=.....(base64)'
      - `application/json `   // '{"avater": "[base64]" }
      - `image/png `  // 
      - `text/plain`
      - `multipart/form-data; boundary=aaa` // Used for form submissions with files
        
  - req body: format need to match with server requirement
    - need to match req head Context-Type
      - req body for 'multipart/form-data; boundary=aaa':
        ```
          --aaa
          Content-Disposition: form-data; name="name"

          John Doe
          --aaa
          Content-Disposition: form-data; name="age"

          28
          --aaa
          Content-Disposition: form-data; name="profile_picture"; filename="photo.jpg"
          Content-Type: image/jpeg

          <binary data of photo.jpg, could be array buffer>
          --aaa--
        ```
  
  <br>
- response has 3 parts
  - res line, e.g. HTTP/1.1 200 OK
    - HTTP/1.1: http version
    - 200: status code
      - 1**: need more info, require more execution from client
      - 2**: success
      - 3**: success with other info (redirect)
        - 301: resource is permanently redirected, recommand not to visit
        - 302: resource is temperarily redirected, probably can be visit in the future
      - 4**: request failed due to client error
      - 5**: server error
    - OK: status text, usually same as res code, controlled by server
  - res head: key-value pair
    - Content-Type: text/html   // res content
    - Context-length: 276   // res size
  - res body


<br>

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
    - Signature: hashing header and payload together with a secret key. The primary goal of the signature is to **ensure that the message has not been altered** during transfer, message can be decoded without signature
- <span>SEO (search engine optimization)</span> :
  - **benifits**: 
    - free of charge
    - organic traffic is typically consistent once ranking is high
    - potential to reach massive audience
  
  - **How google works**
    1. crawling and indexation
       1. google crawlers (spiders) => known urls (seeds) => follow hyperlinks to other pages => repeat
       2. collected data => create search index
   
    2. ranking algorithm
       1. changed 500 - 600 per year (hard to know exactly)
       2. speculated factors:
          1. backlinks: links of a page of one website to another prominent websites
          2. 
---

### ASCII vs Unicode (UTF-8, UTF-16 & UTF-32)
- **encoding standard**: assigning numbers (code point) to graphical characters (*grapheme*)
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
    - **UTF-8**: requires **8**, **16**, **24** or **32** bits (one to four bytes) to encode a Unicode character, unequal size in bytes for each character, save spaces
      - 1 byte for ASCII (compatible): U+0000 to U+007F
      - 2 bytes for U+0080 to U+07FF
      - 3 bytes for Basic  Multilingual Plane (BMP): U+0800 to U+FFFF
      - 4 bytes for characters outside of BMP: U+10000 to U+10FFFF
    - **UTF-16**: requires either **16** or **32** bits to encode a character, different encoding with UTF-8, more efficienty (in storage) for many **non-English BMP chracters** than UTF-8, like *Chinese, Japanese, Korean*, ..., where 2 bytes is enough rather than 3 bytes in UTF-8.
      - 2 bytes: U+0000 to U+FFFF (BMP)
      - 4 bytes: U+10000 to U+10FFFF
    - **UTF-32**: always requires **32** bits to encode a character
      - 4 bytes for every character
      - Simpler processing algorithms, no surrogate pairs (different bytes for different characters)
      - High storage and memory usage, increased bandwidth consumption.
    <br>
  - must use the **same strategy** for decode

### RSA (Rivest–Shamir–Adleman) cryptosystem
1. Give two primes: 
   - p, q // p = 2, q = 7
2. Get product: 
   - n = p * q // n = 14
3. Get the totient (number of positive integers less that n that are relatively prime to n): 
   - $\phi$(n) = (p - 1) * (q - 1); // $\phi$(14) = 6;
4. choose public key e: 
   - 1 < e < $\phi$(n); // e $\in$ [2, 3, 4, 5]
   - e is coprime with n and $\phi$(n); // e = 5
5. choose private key d: 
   - (d * e) === 1 (mod $\phi$(n)); // 5d === 1 (mod 6), d could be 5, 11, 17, ....
<br>

- message: m
- encryption: m^e === c (mod n) // c - cipher text
- decryption: c^d === m (mod n)
<br>

-  

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