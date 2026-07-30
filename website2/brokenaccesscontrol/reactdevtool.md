# Broken access control via React DevTools

There are 2 exploits in this file.

## Context

The website uses React + Vite. A lot of the UI the website loads are through trusting the client, meaning you can **view** stuff unauthorized. (When you refresh, the changes are gone and you are kicked out. Additionally, you cannot edit anything.) 

However, when clicking some buttons, the website brings you to the page without actually refreshing, allowing you to maintain the fake status of the user through different pages.

## Exploitation

### Client-side Admin Status

Using React DevTools, I used the console to change one of the hooks to is_admin = true. When I went to the user dashboard afterwards, the website displayed me as an admin. (However, I could not access the admin panel as it triggered a refresh.)

#### Why this is bad

Note: "you" is referring to a potential malicious attacker on the website.
- If you manage to get a screenshot of yourself having the verified administrator status, you can get other users to believe you. This can lead to them running browser scripts you give them to get their authentication token, or even give them malicious downloads.
- Since the developer would not know about this exploit, they would genuinely believe that you became an admin and you can easily trick them into giving you money.

### Viewing private projects

I used React DevTools to change the value of my user ID to a different user, and managed to enter other users' project as a viewer. This meant I was able to see private code, which was clear broken access control.


Additionally, in public (and private) projects I was able to become an editor (only in the client). That means that none of my changes would actually save, but through my computer I looked like an editor.

#### Why this is bad

- Private code is exposed to malicious users who should never be able to view it.
- Other users can be tricked into thinking their project is compromised.

## The Fix (applies to both)

Rely on your backend instead of the client before serving. The client can easily be manipulated to be trusted but the backend should be the only source of truth.
