# Lack of Rate-Limiting

## Details

When rate-limiting is not present, a DoS and other attacks like brute-forcing are possible. I tested endpoints with 30-50 requests to verify that there was a lack of rate-limiting.

## Exploitation

Not a single endpoint had rate-limiting. From the endpoint to register accounts, logging in to accounts, creating projects, changing my display name, every single one was vulnerable. 


## Why this is bad

A lack of rate-limiting on the login endpoint means anyone could brute-force into accounts. Account registration and project creation would take up database storage, and a lack of rate-limiting means these could expire the developer's free tier and cost them real money. Even changing the display name many times can cause a DoS via resource exhaustion.

## The Fix(es)

Implement per-IP rate-limiting
