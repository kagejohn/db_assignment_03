# Assignment 3

### How it works
Click on the questions to have them fold out.

## 1. Twitter data

<details>
 <summary>1. How many Twitter users are in the database?</summary>
 
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
  
</details>

<details>
 <summary>2. Who are the most active Twitter users (top ten)?</summary>

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

</details>

3. Who are the 

<details>
 <summary>3.1. five most grumpy (most negative tweets) and</summary>
  
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

</details>
	  
<details>
 <summary>3.2. the most happy (most positive tweets)?</summary>

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

</details>

<details>
 <summary>4. Which Twitter users link the most to other Twitter users? (Provide the top ten.)</summary>

  ```
  Query:
    db.tweets.aggregate([
    {
        $match:{text:/@\w+/}
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
        $limit: 10
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
        "user" : "VioletsCRUK",
        "count" : 251.0
    }
    
    /* 4 */
    {
        "user" : "what_bugs_u",
        "count" : 246.0
    }
    
    /* 5 */
    {
        "user" : "tsarnick",
        "count" : 245.0
    }
    
    /* 6 */
    {
        "user" : "SallytheShizzle",
        "count" : 229.0
    }
    
    /* 7 */
    {
        "user" : "mcraddictal",
        "count" : 217.0
    }
    
    /* 8 */
    {
        "user" : "Karen230683",
        "count" : 216.0
    }
    
    /* 9 */
    {
        "user" : "keza34",
        "count" : 211.0
    }
    
    /* 10 */
    {
        "user" : "TraceyHewins",
        "count" : 202.0
    }
  ```
  
</details>

<details>
 <summary>5. Who is are the most mentioned Twitter users? (Provide the top five.)</summary>
 
  ```
  Query:
    db.tweets.aggregate([
    {
        $match: { text: /@\w+/}
    }, 
    {
        $project:
        {
            user:1,
            text: { $split: ["$text", " "] }
        }
    },
    {
        $unwind: "$text"
    },
    {
        $match: { text: /@\w+/}
    }, 
    {
        $project:
        {
            user:1,
            text: { $split: ["$text", "@"] }
        }
    }, 
    {
        $project:
        {
            user:1,
            text: { $arrayElemAt: [ "$text", 1 ] }
        }
    },
    {
        $group:
        {
            _id: "$text",
            user: {$first: "$text"},
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
        "user" : "mileycyrus",
        "count" : 4325.0
    }
    
    /* 2 */
    {
        "user" : "tommcfly",
        "count" : 3841.0
    }
    
    /* 3 */
    {
        "user" : "ddlovato",
        "count" : 3356.0
    }
    
    /* 4 */
    {
        "user" : "Jonasbrothers",
        "count" : 1267.0
    }
    
    /* 5 */
    {
        "user" : "DavidArchie",
        "count" : 1227.0
    }
  ```

</details>


## 2. Modeling

Model | Atomicity | Sharding |Indexes |Large Number of Collections | Collection Contains Large Number of Small Documents
----|:----:|:----:|:----:|:----:|:----:
Arrays of Ancestors	|x|x|x|x||
Materialized paths  |x|x|x|x|x|
Nested sets			|x|x|x|||

### Arrays of Ancestors

#### Atomicity

Will work well for Arrays of Ancestors because documents doesn't contain any information that would have to be changed if something was changed in another document unless changes will be made to _id and that shouldn't really happen.

#### Sharding

Should work as planned so that load can be distributed.

#### Indexes

Will most likley not changed much because each document have all information about its parents, when writing you just need to look at the parent and then you have all the information needed.

#### Large Number of Collections

Could possibly be a good idea were all children of one document would be put in a collection with the parents name but i am acceptably sure it would cause more problems than it would solve.

### Materialized paths

#### Atomicity

Will work well for Materialized paths because documents doesn't contain any information that would have to be changed if something was changed in another document unless changes will be made to _id and that shouldn't really happen.

#### Sharding

Should work as planned so that load can be distributed.

#### Indexes

Will most likley not changed much because each document have all information about its path, when writing you just need to look at the parent and then you have all the information needed.

#### Large Number of Collections

Could possibly be a good idea were all children of one document would be put in a collection with the parents name but i am acceptably sure it would cause more problems than it would solve.

#### Collection Contains Large Number of Small Documents

Could possibly be a good idea but the top documents would quickly get huge.

### Nested sets

#### Atomicity

Will not really work well because if you want to add one document you need to update every single other document in the collection.

#### Sharding

Most likley won't work well because you need to keep a record in every document of its order so adding one document would put load on all shards.

#### Indexes

Will most likely help on read performance because a document only have information about its parent and order.
