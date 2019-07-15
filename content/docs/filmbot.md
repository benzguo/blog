# Filmbot

*2019*

Filmbot scrapes independent movie theater listings in a city and generates a digest of movies playing in the next week. 

https://filmbot.info/

![filmbot](/img/filmbot.png)

The design of the site is "as primitive as possible", optimized for quick skimming, fast iteration, and low maintenance. 

The project started as a weekly email digest, a few scripts cobbled together in an evening. When I was living in New York, I'd run the script manually on Monday mornings, sending the digest to a few dozen subscribers.

Now, Filmbot is a static site deployed from GitHub. A nightly cron runs the crawler and pushes html to git. 
