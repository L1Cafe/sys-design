# Describe HTTP

HTTP (Hypertext Transfer Protocol) is the foundation of data communication on the World Wide Web. It is a protocol that allows web browsers and servers to communicate and exchange information. HTTP is responsible for delivering the content of web pages, including text, images, videos, and other multimedia files.

HTTP is a stateless protocol, which means that each request is processed independently of any previous or future requests. To maintain state across requests, HTTP uses cookies, which are small pieces of data stored on the client-side that can be retrieved by the server. Cookies allow servers to identify users and remember their preferences or other information across multiple requests.

## HTTP connection

1. The user types the website address (URL) in the browser's address bar.
2. The browser converts the URL into an HTTP request message containing the website's hostname and path.
3. The browser performs a DNS (Domain Name System) lookup to obtain the IP address of the server that hosts the website.
4. The browser establishes a TCP (Transmission Control Protocol) connection with the server at the IP address obtained from the DNS lookup.
5. Once the TCP connection is established, the browser sends an HTTP request message to the server containing the website's hostname and path.
6. The server receives the HTTP request message, processes it, and generates an HTTP response message containing the requested content and any relevant metadata.
7. The server sends the HTTP response message back to the browser over the established TCP connection.
8. The browser receives the HTTP response message and parses it to extract the website's content and metadata.
9. The browser then renders the website's content in the browser window for the user to view.

## HTTPS

HTTPS (HTTP Secure) is a variant of HTTP that adds encryption and authentication to the protocol to provide a secure communication channel between the client and server.

HTTPS can use SSL (Secure Sockets Layer) or TLS (Transport Layer Security). TLS is the most widely used encryption mechanism for HTTPS. It is a protocol that encrypts data in transit and provides authentication of the server and client.

HTTPS uses public key infrastructure (PKI) to exchange the encryption keys between the client and server. Here's how the key exchange works:

1. The client sends a request to the server to initiate a TLS handshake.
2. The server responds with its SSL/TLS certificate, which contains its public key and other identifying information.
3. The client verifies the server's SSL/TLS certificate and generates a symmetric session key to use for encrypting the data being transmitted.
4. The client encrypts the session key with the server's public key and sends it back to the server.
5. The server decrypts the session key using its private key and uses it to encrypt the data being transmitted.

HTTPS also includes additional features to improve security, such as HSTS (HTTP Strict Transport Security). HSTS instructs web browsers to always use HTTPS when communicating with a particular website, even if the user enters the website address with HTTP. This helps to prevent man-in-the-middle attacks and other forms of eavesdropping. Additionally, HSTS also includes a mechanism to prevent downgrading attacks, which occur when an attacker attempts to force the use of unencrypted HTTP by intercepting the initial HTTPS request and returning a redirect to an HTTP version of the website.

## Most common HTTP methods

### GET

Retrieves a resource from a server. The server sends the resource in its response.

### POST

Submits data to create or update a resource. The server processes the data and creates or updates the resource.

### PUT

Updates or replaces a resource. The server replaces the resource with the submitted data.

### DELETE

Deletes a resource. The server deletes the specified resource.

### HEAD

Like GET but only retrieves resource metadata, not the resource itself. Useful for getting info without downloading the resource.

