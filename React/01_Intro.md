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
     for https --> HTTPS = HTTP + SSL/TLS encryption. The “S” in HTTPS means that data between client and server is encrypted using TLS (Transport Layer Security). first TCP connection is established and then TLS Handshake (the “Secure” part begins).
  5. The request is sent from client to the server for and the server sends html, css, js in response.
  6. The browser parses HTML --> creates DOM, parses CSS - creates CSSOM, merges both to create a render tree. After that the positioning and sizes is calculated for the elements in the render tree and the the pixels are drawn on the screen. This is how a webpage is displayed on the screen.
  7. If a JS file is seen when parsing HTML, it pauses the parsing and fetches and executes JS first and then continues the parsing of HTML which can cause unusual behaviour. To avoid this you can add the script tag at the bottom of html page or use defer/async attribute. defer means the browser downloads script in parallel with HTML parsing.But execution is deferred until the entire HTML is parsed.	All deferred scripts execute in order of appearance. Scripts are executed after DOM is ready, before DOMContentLoaded. While async makes browser to download script in parallel with HTML parsing. Once the script finishes downloading, browser pauses HTML parsing, executes it immediately, then resumes HTML parsing after. Best for independent scripts (like analytics or ads).
