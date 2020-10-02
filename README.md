Need Help: How to add (if not exists) related records in POST Method.

# Strapi application

Strapi v3.1.6 created with --quickstart (using SQLite)

The Data Model is:

3 Tables - Posts, Categories and Tags.

Posts has and belongs to many Categories
Posts has and belongs to many Tags

In ./tmp.data.db has already example data (few posts,tags and categories)

# What I want to achieve

Adding (if not exists) related records in POST Method.

When I add a new post with categories and tags. If any category or tags does not already exists in db - to be added.

Exact Example:

POST method to http://localhost:1337/posts with body:

```
    {
        "uid": 1111,
        "title": "New article title created by Strapi REST API endpoint",
        "content": "New article content created by Strapi REST API endpoint with POST method...",
        "categories": [
            "Health",
            "NewCat1",
            "NewCat2"
        ],
        "tags": [
            "brain",
            "newTag1",
            "newTag2"
        ]
    }
```

Current response:

```
{
    "id": 5,
    "title": "New article title created by Strapi REST API endpoint",
    "content": "New article content created by Strapi REST API endpoint with POST method...",
    "slug": null,
    "uid": 1111,
    "created_by": null,
    "updated_by": null,
    "created_at": "2020-10-02T07:16:44.581Z",
    "updated_at": "2020-10-02T07:16:44.581Z",
    "categories": [],
    "tags": []
}
```

What I want to be the response:

```
{
    "id": 5,
    "title": "New article title created by Strapi REST API endpoint",
    "content": "New article content created by Strapi REST API endpoint with POST method...",
    "slug": null,
    "uid": 1111,
    "created_by": null,
    "updated_by": null,
    "created_at": "2020-10-02T07:16:44.581Z",
    "updated_at": "2020-10-02T07:16:44.581Z",
    "categories": [
            {
                "id": 3,
                "name": "Health",
                "slug": "health"
            },
                     {
                "id": 6,
                "name": "NewCat1",
                "slug": "newcat1"
            },
                     {
                "id": 7,
                "name": "NewCat2",
                "slug": "newcat2"
            }
     "tags": [
            {
                "id": 7,
                "name": "brain",
                "slug": "brain",
                "created_by": 1,
                "updated_by": 1,
                "created_at": "2020-10-02T05:51:48.013Z",
                "updated_at": "2020-10-02T05:51:48.022Z"
            },
                       {
                "id": 9,
                "name": "newTag1",
                "slug": "newtag1",
                "created_by": 1,
                "updated_by": 1,
                "created_at": "2020-10-02T05:51:48.013Z",
                "updated_at": "2020-10-02T05:51:48.022Z"
            },           {
                "id": 10,
                "name": "newTag2",
                "slug": "newtag1",
                "created_by": 1,
                "updated_by": 1,
                "created_at": "2020-10-02T05:51:48.013Z",
                "updated_at": "2020-10-02T05:51:48.022Z"
            }
        ]
}
```
"Health" category alraedy exists, that's why the ID is 3. "NewCat1" and "NewCat1" doesn't not exists, so they were added in db and got new IDs 6 and 7.
Same as the tags.

If I understand right after making the post request, Strapi in the backend first needs to find the IDs of each Category and Post. If they don't exists - to add them and get back all the IDs of the added categories and posts and then add do the post record like this:

```
{
    "title": "New article title created by Strapi REST API endpoint",
    "content": "New article content created by Strapi REST API endpoint with POST method...",
    "categories": [3,6,7],
    "tags": [7,9,10]
}
```

I've tried with weeks/months to find information (youtube,stackoverflow,github,udemy...), but for my suprise I was not able to find anything showing how to do exactly this. Doesn't matter if it's about Strapi,Feathers,Prisma... If anyone can show me the code how to do this will be huge help for me and other beginners like me.

Thank you.
