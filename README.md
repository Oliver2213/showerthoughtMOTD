# ShowerthoughtMOTD - get a random showerthought from the subreddit with the same name

I use this script in my MOTD for amusement and more than ocasionally a really deep or interesting thought.

## Requirements

* Python, 2 or 3 should work.
* [Praw](https://praw.readthedocs.io/en/stable/).
* A dynamic MOTD.
* cron or something similar

## Getting a dynamic MOTD

* If you're using a modern version of Ubuntu, you should have this already, and you can just drop the script in /etc/update-motd.d, with a name like '30-showerthought', depending on what else is there and in what order you want it to appear in the final result.
* If using debian 8, you have a bit more work to do:
  * sudo rm -f /etc/motd
  * sudo ln -s /var/run/motd /etc/motd
  * sudo mkdir /etc/update-motd.d
  * Now you can copy and rename the script into /etc/update-motd.d with whatever sequence number you please.

### NOTE

Make sure *all* your scripts in /etc/update-motd.d are executable with: sudo chmod +x /etc/update-motd.d/*

## Setting up caching

Originally, this script retrieved a thought every time a dynamic MOTD was created (every time someone logs into the system, run-parts /etc/update-motd.d gets executed by a pam module). 
I found that this was just much too slow for my liking, so I made the showerthought_cache script, that you can run with cron or something similar. It gets and stores (by default) 100 "thoughts" and then exits, and the main showerthought script, whether being run manually or by the dynamic MOTD, will use the cache. Much faster.

To set this up, simply copy showerthought_cache to /usr/bin or somewhere similar, make sure it's executable, and after typing sudo crontab -e:

```
0 */2 * * * /usr/bin/showerthought_cache
```

Will set things up so the cache gets refreshed every 2 hours. You can, of course, set this how you like.

## Customization

* To change where the caching script saves it's "thoughts", set the showerthought_dir variable in the aforementioned script to the directory where you want the file to reside (it will be created if it doesn't already exist). 
* To change the filename itself, change the showerthought_cfn variable in the same script.
* to change how many "thoughts" are cached on each script run, set the showerthought_limit variable. This is also mentioned in the file, but... The limit for one API call to reddit is 100 items; 2 seconds between API requests means each hundred you increase the limit by will raise the time this script runs by at least 2 seconds. Therefore, depending on how often you have cron refresh the cache, you may want to lower / raise the limit. If the refresh time is shorter, you'll probably want the limit to be lower, and if the refresh time is longer, a higher limit would give you more "thoughts" for the motd to randomize.

###Note

If you change the location or filename of the cache, remember to change the showerthought script as well so it knows where to look.
