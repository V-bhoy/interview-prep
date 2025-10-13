## How does browser work?
- URL --> protocol + domain name (host, second level domain, top level domain)
- ```https://www.example.com``` --> https = protocol, www = host, example = second level domain, com = top level domain.
- When you enter the URL in the browser:
  1. it checks whether the url is valid or not, if it is invalid, it will show a page like site not found.
  2. if it is valid, DNS lookup happens --> it checks for the IP address of the domain name in the browser cache, OS cache, router cache, ISP cache. If it is not found anywhere it queries the top level domain first for its IP and then the second level domain from the server of the IP that was previously received. Once you get the IP of the domain, it is stored in the cache of ISP.
  3. Connection between client & server is established. It checks the protocol which can be http, https, ftp etc. and based on the protocol the connection is established. For example: for http protocol, a TCP connection is established (3 way handshake).
  ```
  TCP must establish a reliable connection.
	1.	SYN → Client sends SYN packet to server (wants to start connection)
	2.	SYN-ACK ← Server acknowledges and responds
	3.	ACK → Client acknowledges back

  ✅ Now TCP connection is established.
  ```
     for https --> HTTPS = HTTP + SSL/TLS encryption. The “S” in HTTPS means that data between client and server is encrypted using TLS (Transport Layer Security) for transporting data securely from client to server. First TCP connection is established and then TLS Handshake (the “Secure” part begins). TLS is the successor to SSL. It ecrypts data and ensures its integrity, confidentiality and authenticity between client and server.
  ```
  - when it establishes TLS handshake, it acquires a public key from the server to encrypt the data and the server decrypts it using a private key.
  For data confidentiality --> data accessed only by client/server, other human if tries to access cannot read it --> encryption is used
  2 types of encryption -->
  1. symmetric
      - same key is used to encrypt & decrypt
      - more fast & efficients, generally used fro transporting large data
      - challenging key distribution because single key must be kept a secret.
  2. asymmetric
      - different key is used to encrypt & decrypt
      - slow, used for small data
      - secure even if the public key is shared.
  3. hybrid
      - asymmetric encryption is used to exchange the keys and after that, symmetric encryption is used to transport huge data.
  For data integrity --> no modification in between --> hashing is used
  - process of converting data into fixed size string of characters, sequemce of numbers & letters after adding a secret key, which makes it more secure. Altogether called message auth code (Message + Code)
  For data authentication --> for verifying the identity of the parties who they are supposed to be --> certificates is used
  CA - Certificate Authority
  - trusted organization that issues digital certificates to verify the identity of websites and enable secure, encrypted communication over the internet. It ensures the integrity and authenticity of the SSL certificates they provide.
  - The organization provides public key with other metadata about the organiztion to the CA ans CA on the basis of that issues a certificate to the website that includes the public key & domain identity (a digital signature).
  - Once the SSL certificate is received, when establishing a connection, it send this certificate to the browser and browser first checks if the certificate is valid or not.
  Here’s the sequence:
   CLIENT (Browser)                                  SERVER (Backend)
  ─────────────────────────────────────────────────────────────────────────────
  1️⃣  DNS lookup: "codesip.in" → IP address
  ─────────────────────────────────────────────────────────────────────────────
  2️⃣  TCP 3-way handshake (SYN → SYN-ACK → ACK)
   ✅ TCP connection established (but not yet secure)
  ─────────────────────────────────────────────────────────────────────────────
  3️⃣  TLS Handshake begins
  ─────────────────────────────────────────────────────────────────────────────
  Client Hello  ───────────────────────────────────────────→
   • Supported TLS versions (1.3, 1.2…)
   • Supported cipher suites (encryption algorithms)
   • Random value (ClientRandom)

                                      Server Hello  ←──────────────────────────
                                         • Chosen TLS version & cipher suite
                                         • Random value (ServerRandom)
                                         • Server's SSL Certificate 
                                             ↳ Contains Public Key
                                             ↳ Signed by Certificate Authority (CA)

  ─────────────────────────────────────────────────────────────────────────────
  4️⃣  Browser verifies certificate:
   • Checks CA signature
   • Confirms domain name
   • Confirms certificate not expired/revoked

  If ✅ verified → continue handshake  
  If ❌ invalid → “⚠️ Connection not secure” error

  ─────────────────────────────────────────────────────────────────────────────
   5️⃣  Key Exchange (Asymmetric encryption)
  ─────────────────────────────────────────────────────────────────────────────
  Browser generates a **Session Key** (a random symmetric key)
  It’s used for the upcoming encrypted communication.

  Client encrypts Session Key with Server’s **Public Key**
  and sends it securely:

  Encrypted(Session Key, Public Key) ───────────────→

  Server receives it and uses its **Private Key** to decrypt:
  Decrypted(Session Key, Private Key)

  ✅ Now both browser and server have the same Session Key.

  ─────────────────────────────────────────────────────────────────────────────
  6️⃣  Secure channel established 🔐
  ─────────────────────────────────────────────────────────────────────────────
  Both sides now use the **Session Key** (symmetric encryption)
  for all further data:

  GET /home (encrypted with Session Key) ──────────→
  <html>...</html> (encrypted with Session Key) ←──────

  Because symmetric encryption is very fast,
  this keeps the communication both secure & efficient.

  ─────────────────────────────────────────────────────────────────────────────

  ✅ Now the secure TLS tunnel is established.
  Once the TLS handshake is done:
	•	All HTTP requests (GET, POST, etc.) and responses are encrypted.
	•	Even if someone intercepts packets, they only see encrypted gibberish.
  
  https://youtu.be/EnY6fSng3Ew?si=Fm-gXScLZi12diAy
  ```
  
  4. The request is sent from client to the server for and the server sends html, css, js in response.
  5. The browser parses HTML --> creates DOM, parses CSS - creates CSSOM, merges both to create a render tree. Each node has both content and style information. After that the positioning and sizes is calculated for the elements in the render tree and the the pixels are drawn on the screen. Finally, all layers are combined into one final image displayed on your screen. This is how a webpage is displayed on the screen.
  6. If a JS file is seen when parsing HTML, it pauses the parsing and fetches and executes JS first and then continues the parsing of HTML which can cause unusual behaviour. To avoid this you can add the script tag at the bottom of html page or use defer/async attribute. defer means the browser downloads script in parallel with HTML parsing.But execution is deferred until the entire HTML is parsed.	All deferred scripts execute in order of appearance. Scripts are executed after DOM is ready, before DOMContentLoaded. While async makes browser to download script in parallel with HTML parsing. Once the script finishes downloading, browser pauses HTML parsing, executes it immediately, then resumes HTML parsing after. Best for independent scripts (like analytics or ads).

## What is critical rendering path in a browser?
- The Critical Rendering Path is the sequence of steps a browser takes to convert HTML, CSS, and JavaScript into pixels on the screen — i.e., how a web page goes from code → actual visible UI. The faster this path completes, the faster your page appears to the user.
- By default:
   - CSS files are render-blocking — the browser must wait for them before it can render content (since it can’t paint without knowing styles).
   - JavaScript files can also block rendering (since they may modify the DOM or CSSOM).

## How to optimize the critical rendering path?
- Minimize critical resources - Only load what’s needed for initial view.
- Defer non-critical JS - Use defer or async to prevent blocking rendering.
- Inline critical CSS - Embed small, above-the-fold CSS directly in HTML.
- Lazy load images - Load below-the-fold images later.
- Use caching & compression - Reduce network time.

## What is progressive rendering?
- Progressive Rendering is a performance optimization technique where a web page is rendered and displayed to the user in chunks (progressively) — instead of waiting for the entire page and all its resources to load first. Show users something as soon as possible rather than making them wait for the full page to be ready.
