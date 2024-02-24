FeedGeneration:

1. The feed generation API creates a news feed my retrieving all relevant posts, by friends, your own, or through groups you are a member of, and stores and filters them by creating a priority Queue that prioritized posts on the bases of date and filters the top 50 posts and stores it in redis for faster retrial. Also store the max date of post, this will be used when we need to refresh the news feed

Sudo Code:

pq = PriorityQueue

user_friends_list
user_id
user_groups_list

pq = run_query(Select \* from Post where userId = userId or userId in user_friends_list or posted_group = user_groups_list order by date)

pq.filter(50)
max_date_of_post = pq.max(post.date)

FeedRefresh:

2. Whenever a user refreshes his/her feed, we check the database against the same criteria as before but this time we only get posts that where posted after the max_date_of_post to only get the newly added posts and remove the least prioritized posts from the list

new_posts = Select \* from Post where (userId = userId or userId in user_friends_list or posted_group = user_groups_list) and date > max_date_of_post order by date

pq.removeFromEnd(len(new_posts))
pq.append(new_posts)
