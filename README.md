# Assignment 3

## 1. Twitter data
1. How many Twitter users are in the database?

  ```
  Query:
	db.tweets.aggregate([
	{
        $group: { _id: "$user" }
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
        $sort: { count: -1 }
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

	  3.1. five most grumpy (most negative tweets) and
  
  ```
  Query:
	db.tweets.aggregate([
	{ 
	    $match: { polarity: 0 } 
	},
	{
	    $group:
        {
            _id: "$user",
            user: {$first: "$user"},
            count: { $sum:1 }
        }
	},
	{
	    $sort: { count: -1 }
	},
	{ 
	    $project: 
	    {
	        _id:0,
	        user:1,
	        count:1 
	    } 
	},
	{ 
	    $limit: 5
    }
	])
  ```
  
  ```
  Response:
	/* 1 */
	{
	    "user" : "lost_dog",
	    "count" : 549.0
	}

	/* 2 */
	{
	    "user" : "tweetpet",
	    "count" : 310.0
	}

	/* 3 */
	{
	    "user" : "webwoke",
	    "count" : 264.0
	}

	/* 4 */
	{
	    "user" : "mcraddictal",
	    "count" : 210.0
	}

	/* 5 */
	{
	    "user" : "wowlew",
	    "count" : 210.0
	}
  ```
  
3.2. the most happy (most positive tweets)?

  ```
  Query:
	db.tweets.aggregate([
	{ 
	    $match: { polarity: 4 } 
	},
	{
	    $group:
        {
            _id: "$user",
            user: {$first: "$user"},
            count: { $sum:1 }
        }
	},
	{
	    $sort: { count: -1 }
	},
	{
	    $limit: 5
	},
	{ 
	    $project: 
	    { 
	        _id:0,
	        user:1,
	        count:1
        } 
	}
	])
  ```
  
  ```
  Response:
	/* 1 */
	{
	    "user" : "what_bugs_u",
	    "count" : 246.0
	}

	/* 2 */
	{
	    "user" : "DarkPiano",
	    "count" : 231.0
	}

	/* 3 */
	{
	    "user" : "VioletsCRUK",
	    "count" : 218.0
	}

	/* 4 */
	{
	    "user" : "tsarnick",
	    "count" : 212.0
	}

	/* 5 */
	{
	    "user" : "keza34",
	    "count" : 211.0
	}
  ```
4. Which Twitter users link the most to other Twitter users? (Provide the top ten.)
5. Who is are the most mentioned Twitter users? (Provide the top five.)

## 2. Modeling
TODO
