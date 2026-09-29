# Client side trust

## Details

The website has a quiz feature, and would record the amount of time you took to answer the question.

## Exploitation

I found out through Burp Suite the time taken was actually passed in the JSON body. This meant I could change my time to 1 second, or even 0 seconds.

## Why this is bad

If the developer of the website builds a leaderboard feature for people taking the quiz, people who take a very long time to answer the questions (or take long times because they searched google) can simply change their timing to 0 or negative seconds and be at the top of the leaderboard.

Additionally, people taking the quiz can fool the person assigning them the quiz by changing how much time they took.

## The fix

Record how much time the quiz-taker takes on the server side, not the client side.
