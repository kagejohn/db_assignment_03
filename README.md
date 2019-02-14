# Assignment 3

## 1. Twitter data
1. How many Twitter users are in the database?

  ```
  Query:
	db.tweets.aggregate([
	{
        $group:
        {
            _id: "$user"
        }
    },
    {
        $count: "count"
    }
	])
  ```

  ```
  Response:
	{
		"count" : 659774
	}
  ```

2. Who are the most active Twitter users (top ten)?

  ```
  Query:
	db.tweets.aggregate([
	{
        $group:
        {
            _id: "$user",
            count: { $sum:1 }
        }
    },
    {
        $sort:
        {
            count: -1
        }
    },
    {
        $limit: 10
    }
	])
  ```

  ```
  Response:
	/* 1 */
	{
	    "_id" : "lost_dog",
	    "count" : 549.0
	}

	/* 2 */
	{
	    "_id" : "webwoke",
	    "count" : 345.0
	}

	/* 3 */
	{
	    "_id" : "tweetpet",
	    "count" : 310.0
	}

	/* 4 */
	{
	    "_id" : "SallytheShizzle",
	    "count" : 281.0
	}

	/* 5 */
	{
	    "_id" : "VioletsCRUK",
	    "count" : 279.0
	}

	/* 6 */
	{
	    "_id" : "mcraddictal",
	    "count" : 276.0
	}

	/* 7 */
	{
	    "_id" : "tsarnick",
	    "count" : 248.0
	}

	/* 8 */
	{
	    "_id" : "what_bugs_u",
	    "count" : 246.0
	}

	/* 9 */
	{
	    "_id" : "Karen230683",
	    "count" : 238.0
	}

	/* 10 */
	{
	    "_id" : "DarkPiano",
	    "count" : 236.0
	}
  ```

3. Who are the 
	  * five most grumpy (most negative tweets) and 
	  * the most happy (most positive tweets)? 
4. Which Twitter users link the most to other Twitter users? (Provide the top ten.)
5. Who is are the most mentioned Twitter users? (Provide the top five.)

## 2. Modeling
TODO
