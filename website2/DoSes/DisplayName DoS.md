# Display Name DoS

## Exploitation

Just like how registering thousands of accounts can easily exhaust a server, other **seemingly insignificant** endpoints can also cause this.

For example, the endpoint to change your display name on the website. It seems like a minor feature with not much to it, but it still does send a PATCH request and changes data in the database.

Using JavaScript code to paste in the console for the async function, I managed to change my name 5,000 times, easily causing a Denial of Service in the website.

## Fix

Implement rate-limiting per user for this endpoint, about 2/min for a strict rate-limit.

Ensure you add rate-limiting for every single endpoint, no matter how insignificant.
