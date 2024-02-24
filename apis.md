FeedGeneration:

1. The feed generation API creates a news feed my retrieving all relevant posts, by friends, your own, or through groups you are a member of, and stores and filters them by creating a priority Queue that prioritized posts on the bases of date and filters the top 50 posts and stores it in redis for faster retrial.

Sudo Code:

pq = PriorityQueue

user_friends_list
user_id
user_groups_list

pq = run_query(Select \* from Post where userId = userId or userId in user_friends_list or posted_group = user_groups_list order by date)

pq.filter(50)
