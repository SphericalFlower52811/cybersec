# DoS through websockets

## Exploitation

The website being tested on uses WebSockets for the real-time collaboration element.

Opening many websockets at a time will easily exhaust the server, so I wanted to try it out with JavaScript code (which was lost) pasted in the console to open 1,000,000 websocket connections, causing a DoS.

## Fix

Implement per-IP rate-limiting.
