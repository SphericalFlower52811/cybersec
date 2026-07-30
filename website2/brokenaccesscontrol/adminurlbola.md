# Admin Panel BOLA

## How it was exploited

At this time, I had just installed Burp suite. I used burp suite to intercept to the request to the admin endpoint, only to realise the backend verified you using the endpoint /admin/users/${userId}, and that I simply had to change the ID field to 4 (his user ID), and I got into the admin panel as him.

## How to fix

I told him the fix was to implement proper backend authentication instead of relying on the client, and he changed to JWTs (JSON Web Tokens) with a secure signature.
