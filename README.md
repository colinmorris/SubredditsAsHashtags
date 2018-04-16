Analyzing the phenomenon of 'subreddits as hashtags' - when reddit users leave comments consisting only of a subreddit name as a form of commentary. Subreddits commonly used for this purpose include /r/nocontext, /r/thathappened, and /r/titlegore.

## Files

- `top_hts_comms.csv`: The 15k most frequently hashtagged subreddits, with the number of times they've been hashtagged ('tot'), and the total number of comments posted in the actual subreddit, as a measure of its level of activity.
- `lt_10k_comments_top_hts.csv`: The most commonly hashtagged low-activity subreddits (having less than 10k total comments).
- `long_subs.csv`: hashtagged subreddits sorted by length of subreddit name. `long_subs_gt_2.csv` is the same thing, but only subreddits that have been hashtagged more than a couple of times.
- `15k_unique_hts.csv`: a random sample of 15,000 subreddit names which have been hashtagged only once (case sensitive). Most aren't actual subreddits.
- `context.csv`: hashtagged subreddits with 'context' in their name
- `theydidthe.csv`: hashtagged subreddit names that are variants on the 'they did the [monster] math' snowclone.

## Numbers

- 380k distinct hashtags (case sensitive). 325k after lowercasing.
  - 280k appear only once. 35k twice, ~40k 3-10 times.

## Methodology

All this data was gathered from the Reddit comments dataset hosted on Google BigQuery [here](https://bigquery.cloud.google.com/dataset/fh-bigquery:reddit_comments).

- RE used was `'^\s*/[rR]/[[:alnum:]]*\s*$'`
  - probably should have made leading and trailing forward slashes optional (but leading slash and no trailing slash is the most common format by far)
  - also this wouldn't have caught cases where people linkified the subreddit name in markdown (though I don't think this is that common?)
  - running the query that builds the hashtags table by running this RE against every comment body eats through about .8 TB, which is about $4 worth, or most of the free limit for one month.
- case preserved in the initial intermediate table, but most of the files in this repo are post-lowercasing and merging
