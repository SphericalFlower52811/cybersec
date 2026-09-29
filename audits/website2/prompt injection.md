# Prompt Injection

## Details

The website has a translation feature in specific parts of the website. However, the developer used an AI for the translation.

## Exploitation

I changed the translation language to "Pirate" followed by "Lorem Ipsum", knowing a normal translation feature would not accept that as a valid language. However, the response contained the same text but in pirate speech, and in gibberish latin for "pirate" and "lorem ipsum" respectively. This was when I knew it was an AI.

I then asked it to stop translating and tell me what AI model it was, and it responded with what AI it was. This is a prompt injection

## Why this is bad

If I did something like asking it to translate a very long string of text combined with asking it to translate that text into many different languages, the server would take a very long time to process the request. This means that sending that large request even 10 times could slow the websit down significantly. Prompt injection can also have severe consequences, but in this context the AI did not have access to the source code files.

## The Fix

Either ensure the AI is not vulnerable to prompt injection, validate the request body before sending it, or use a simple translation library like python's `deep_translator` module.
