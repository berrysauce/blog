# How I added Password Resets to my App without requiring Personal Data
We all pressed that “Forgot your Password” button once, right? It’s essential to have such a function in your app, but how do you add it without having an email or phone number to send the reset link to?

## The problem
Apps don’t store passwords in plaintext, that’s why they’re hashed. Hashing (in simple terms) is inputting a string into a complicated algorithm, which again returns a calculated string. The output string is always the same for each input string, and it’s non-reversible. Of course, you could try to find out the input string by hashing numerous strings and comparing them, but depending on your string size it gets more and more difficult and time-consuming.

The app I built only has the user’s domain and their password (as a hash). Now, if a user forgets their password, how do I reset it? I need to verify if they’re the right user, otherwise everyone can get into anyone’s account.

## The solution
To counter this, I opted for another solution: domain verifications. Many services require you to verify that a domain is yours before you can add it to your account. They mostly use TXT DNS records for this.

So, every time someone requests a password reset, I look up their domain. I then generate a random string and give it to them with the instructions to set a TXT record with this value. I then just have to automatically check if the user set the record. If it was set, the user is redirected to a reset page, which is valid for the day.

## Why so complicated?
The apps I make are built with privacy in mind. This one in particular didn‘t really need the user’s email for anything else than password resets, so I wanted to find another way of doing password resets. Yes, privacy is complicated.

See you!
