# Showerthought - get a random showerthought from the subreddit with the same name
I use this script in my MOTD for amusement and more than ocasionally a really deep or interesting thought.

## Requirements

* Python, 2 or 3 should work.
* [Praw](https://praw.readthedocs.io/en/stable/).
* A dynamic MOTD.

## Getting a dynamic MOTD

* If you're using a modern version of Ubuntu, you should have this already, and you can just drop the script in /etc/update-motd.d, with a name like '30-showerthought', depending on what else is there and in what order you want it to apper in the final result.
* If using debian 8, you have a bit more work to do:
  * sudo rm -f /etc/motd
  * sudo ln -s /var/run/motd /etc/motd
  * sudo mkdir /etc/update-motd.d
  * Now you can copy and rename the script into /etc/update-motd.d with whatever sequence number you please.

### NOTE

Make sure *all* your scripts in /etc/update-motd.d are executable with: sudo chmod +x /etc/update-motd.d/*

