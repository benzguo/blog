# Filmbot

*2019*

Filmbot scrapes independent movie theater listings in a city and generates a digest of movies playing in the next week. 

https://filmbot.info/

![filmbot](/img/filmbot.png)

The design of the site is "as primitive as possible", optimized for quick skimming, fast iteration, and low maintenance. 

The project started as a weekly email digest, a few scripts cobbled together in an evening. When I was living in New York, I'd run the script manually on Monday mornings, sending the digest to a few dozen subscribers.

The project has evolved a bit since then, after a 2 year hiatus. I've abandoned the mailing list, and done a bit of work to set up a nightly crawl and continuous deploy.

The static site (just a few html pages) is auto-deployed by pushes to GitHub. A nightly cron (1am PST) runs the crawler and pushes updated html files.

This pattern, a "static cron site", seems like it could be applied to a large set of primitive, low maintenance sites. 

Quickstart hosting services like [Render](https://render.com/) (which I use for this project) support auto deploys by pulling from GitHub, but don't support pushing to GitHub. This isn't very hard to set up via the GitHub API, but it would have been nice to be able to set up "auto-push" at the end of running a cron job. 

I think there may something worth exploring here: if you could make scraping the web and creating digests more accessible, is there a set of useful community tools that would emerge organically? 

- [Scrapy](https://scrapy.org/)
- [Why isn't the internet more fun and weird?](https://jarredsumner.com/codeblog/)
- [Craigslist is ugly, janky, old school, and unbeatable](https://www.wired.com/2017/02/craigslist-is-ugly-janky-old-schooland-unbeatable/)
