# Assignment 3

## 1. Twitter data
1. How many Twitter users are in the database?

  ```
  db.tweets.aggregate([
      {
          $group:
              {
                  _id: "$id"
              }
      },
      {
          $group:
              {
                  _id: null,
                  count: { $sum:1 }
              }
      }
  ])
  ```
  
  ```
  {
      "_id" : null,
      "count" : 1598315.0
  }
  ```

2. Who are the most active Twitter users (top ten)?
3. Who are the 
	  * five most grumpy (most negative tweets) and 
	  * the most happy (most positive tweets)? 
4. Which Twitter users link the most to other Twitter users? (Provide the top ten.)
5. Who is are the most mentioned Twitter users? (Provide the top five.)

## 2. Modeling
TODO
