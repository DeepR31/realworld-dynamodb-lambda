```
DELETE /__TESTUTILS__/purge
```
```
200 OK

"Purged all data!"
```
# Article
```
POST /users

{
  "user": {
    "email": "author-fsdlm5@email.com",
    "username": "author-fsdlm5",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "author-fsdlm5@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImF1dGhvci1mc2RsbTUiLCJpYXQiOjE2MTI0MDUzMDQsImV4cCI6MTYxMjU3ODEwNH0.7xFb7vZ2gvDaFwXcZaCcGrQa3W-GxaDeL_3y3wDxcqM",
    "username": "author-fsdlm5",
    "bio": "",
    "image": ""
  }
}
```
```
POST /users

{
  "user": {
    "email": "authoress-gvwrjp@email.com",
    "username": "authoress-gvwrjp",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "authoress-gvwrjp@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImF1dGhvcmVzcy1ndndyanAiLCJpYXQiOjE2MTI0MDUzMDQsImV4cCI6MTYxMjU3ODEwNH0.rRjr8tA5KOW_rX_de6k3WQ7dNociiAjaI0vH-KEnUqw",
    "username": "authoress-gvwrjp",
    "bio": "",
    "image": ""
  }
}
```
```
POST /users

{
  "user": {
    "email": "non-author-1pv8u5@email.com",
    "username": "non-author-1pv8u5",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "non-author-1pv8u5@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6Im5vbi1hdXRob3ItMXB2OHU1IiwiaWF0IjoxNjEyNDA1MzA0LCJleHAiOjE2MTI1NzgxMDR9.vtz4es_RDol7U6heRnWYv-TGnDSEo5LjhKXxllv_Qm0",
    "username": "non-author-1pv8u5",
    "bio": "",
    "image": ""
  }
}
```
## Create
### should create article
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body"
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-tgb7hr",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1612405305211,
    "updatedAt": 1612405305211,
    "author": {
      "username": "author-fsdlm5",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
### should create article with tags
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "tag_a",
      "tag_b"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-4tbp2f",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1612405305262,
    "updatedAt": 1612405305262,
    "author": {
      "username": "author-fsdlm5",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
### should disallow unauthenticated user
```
POST /articles

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should enforce required fields
```
POST /articles

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article must be specified."
    ]
  }
}
```
```
POST /articles

{
  "article": {}
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "title must be specified."
    ]
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "description must be specified."
    ]
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "body must be specified."
    ]
  }
}
```
## Get
### should get article by slug
```
GET /articles/title-tgb7hr
```
```
200 OK

{
  "article": {
    "createdAt": 1612405305211,
    "author": {
      "username": "author-fsdlm5",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "slug": "title-tgb7hr",
    "updatedAt": 1612405305211,
    "tagList": [],
    "favoritesCount": 0,
    "favorited": false
  }
}
```
### should get article with tags by slug
```
GET /articles/title-4tbp2f
```
```
200 OK

{
  "article": {
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "createdAt": 1612405305262,
    "author": {
      "username": "author-fsdlm5",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "slug": "title-4tbp2f",
    "updatedAt": 1612405305262,
    "favoritesCount": 0,
    "favorited": false
  }
}
```
### should disallow unknown slug
```
GET /articles/8v4kw
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [8v4kw]"
    ]
  }
}
```
## Update
### should update article
```
PUT /articles/title-4tbp2f

{
  "article": {
    "title": "newtitle"
  }
}
```
```
200 OK

{
  "article": {
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "createdAt": 1612405305262,
    "author": {
      "username": "author-fsdlm5",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "newtitle",
    "body": "body",
    "slug": "title-4tbp2f",
    "updatedAt": 1612405305262,
    "favoritesCount": 0,
    "favorited": false
  }
}
```
```
PUT /articles/title-4tbp2f

{
  "article": {
    "description": "newdescription"
  }
}
```
```
200 OK

{
  "article": {
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "createdAt": 1612405305262,
    "author": {
      "username": "author-fsdlm5",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "newdescription",
    "title": "newtitle",
    "body": "body",
    "slug": "title-4tbp2f",
    "updatedAt": 1612405305262,
    "favoritesCount": 0,
    "favorited": false
  }
}
```
```
PUT /articles/title-4tbp2f

{
  "article": {
    "body": "newbody"
  }
}
```
```
200 OK

{
  "article": {
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "createdAt": 1612405305262,
    "author": {
      "username": "author-fsdlm5",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "newdescription",
    "title": "newtitle",
    "body": "newbody",
    "slug": "title-4tbp2f",
    "updatedAt": 1612405305262,
    "favoritesCount": 0,
    "favorited": false
  }
}
```
### should disallow missing mutation
```
PUT /articles/title-4tbp2f

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article mutation must be specified."
    ]
  }
}
```
### should disallow empty mutation
```
PUT /articles/title-4tbp2f

{
  "article": {}
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "At least one field must be specified: [title, description, article]."
    ]
  }
}
```
### should disallow unauthenticated update
```
PUT /articles/title-4tbp2f

{
  "article": {
    "title": "newtitle"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should disallow updating non-existent article
```
PUT /articles/foo-title-4tbp2f

{
  "article": {
    "title": "newtitle"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [foo-title-4tbp2f]"
    ]
  }
}
```
### should disallow non-author from updating
```
PUT /articles/title-4tbp2f

{
  "article": {
    "title": "newtitle"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article can only be updated by author: [author-fsdlm5]"
    ]
  }
}
```
## Favorite
### should favorite article
```
POST /articles/title-tgb7hr/favorite

{}
```
```
200 OK

{
  "article": {
    "createdAt": 1612405305211,
    "author": {
      "username": "author-fsdlm5",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "slug": "title-tgb7hr",
    "updatedAt": 1612405305211,
    "favoritedBy": [
      "non-author-1pv8u5"
    ],
    "favoritesCount": 1,
    "tagList": [],
    "favorited": true
  }
}
```
```
GET /articles/title-tgb7hr
```
```
200 OK

{
  "article": {
    "createdAt": 1612405305211,
    "author": {
      "username": "author-fsdlm5",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "favoritesCount": 1,
    "slug": "title-tgb7hr",
    "updatedAt": 1612405305211,
    "tagList": [],
    "favorited": true
  }
}
```
### should disallow favoriting by unauthenticated user
```
POST /articles/title-tgb7hr/favorite

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should disallow favoriting unknown article
```
POST /articles/title-tgb7hr_foo/favorite

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [title-tgb7hr_foo]"
    ]
  }
}
```
### should unfavorite article
```
DELETE /articles/title-tgb7hr/favorite
```
```
200 OK

{
  "article": {
    "createdAt": 1612405305211,
    "author": {
      "username": "author-fsdlm5",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "favoritesCount": 0,
    "slug": "title-tgb7hr",
    "updatedAt": 1612405305211,
    "tagList": [],
    "favorited": false
  }
}
```
## Delete
### should delete article
```
DELETE /articles/title-tgb7hr
```
```
200 OK

{}
```
```
GET /articles/title-tgb7hr
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [title-tgb7hr]"
    ]
  }
}
```
### should disallow deleting by unauthenticated user
```
DELETE /articles/foo
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should disallow deleting unknown article
```
DELETE /articles/foobar
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [foobar]"
    ]
  }
}
```
### should disallow deleting article by non-author
```
DELETE /articles/title-4tbp2f
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article can only be deleted by author: [author-fsdlm5]"
    ]
  }
}
```
## List
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "ufkf2m",
      "tag_0",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-p9sh4v",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1612405306157,
    "updatedAt": 1612405306157,
    "author": {
      "username": "authoress-gvwrjp",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "ufkf2m",
      "tag_0",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "gwibbd",
      "tag_1",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-lvdap4",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1612405306217,
    "updatedAt": 1612405306217,
    "author": {
      "username": "author-fsdlm5",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "gwibbd",
      "tag_1",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "q2c37m",
      "tag_2",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-ks960d",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1612405306249,
    "updatedAt": 1612405306249,
    "author": {
      "username": "authoress-gvwrjp",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "q2c37m",
      "tag_2",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "p6wgj7",
      "tag_3",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-89c206",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1612405306275,
    "updatedAt": 1612405306275,
    "author": {
      "username": "author-fsdlm5",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "p6wgj7",
      "tag_3",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "tafj9g",
      "tag_4",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-srtkro",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1612405306302,
    "updatedAt": 1612405306302,
    "author": {
      "username": "authoress-gvwrjp",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "tafj9g",
      "tag_4",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "9dy7tg",
      "tag_5",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-mqatk",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1612405306327,
    "updatedAt": 1612405306327,
    "author": {
      "username": "author-fsdlm5",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "9dy7tg",
      "tag_5",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "y20oky",
      "tag_6",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-q46fax",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1612405306352,
    "updatedAt": 1612405306352,
    "author": {
      "username": "authoress-gvwrjp",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "y20oky",
      "tag_6",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "y9aezi",
      "tag_7",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-f93syh",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1612405306378,
    "updatedAt": 1612405306378,
    "author": {
      "username": "author-fsdlm5",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "y9aezi",
      "tag_7",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "ljg2t7",
      "tag_8",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-g4ewyg",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1612405306410,
    "updatedAt": 1612405306410,
    "author": {
      "username": "authoress-gvwrjp",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "ljg2t7",
      "tag_8",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "inlxwa",
      "tag_9",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-1q5lz9",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1612405306441,
    "updatedAt": 1612405306441,
    "author": {
      "username": "author-fsdlm5",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "inlxwa",
      "tag_9",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "kzw7ti",
      "tag_10",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-t9ehkb",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1612405306467,
    "updatedAt": 1612405306467,
    "author": {
      "username": "authoress-gvwrjp",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "kzw7ti",
      "tag_10",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "s8osai",
      "tag_11",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-oqjmzy",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1612405306490,
    "updatedAt": 1612405306490,
    "author": {
      "username": "author-fsdlm5",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "s8osai",
      "tag_11",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "yhhefy",
      "tag_12",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-6tiqk1",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1612405306513,
    "updatedAt": 1612405306513,
    "author": {
      "username": "authoress-gvwrjp",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "yhhefy",
      "tag_12",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "fdv9o2",
      "tag_13",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-jbhxbn",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1612405306539,
    "updatedAt": 1612405306539,
    "author": {
      "username": "author-fsdlm5",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "fdv9o2",
      "tag_13",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "lsptn9",
      "tag_14",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-p6jf1b",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1612405306562,
    "updatedAt": 1612405306562,
    "author": {
      "username": "authoress-gvwrjp",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "lsptn9",
      "tag_14",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "wlg39v",
      "tag_15",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-sfdpdq",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1612405306587,
    "updatedAt": 1612405306587,
    "author": {
      "username": "author-fsdlm5",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "wlg39v",
      "tag_15",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "dbdb4v",
      "tag_16",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-ka05x6",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1612405306620,
    "updatedAt": 1612405306620,
    "author": {
      "username": "authoress-gvwrjp",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "dbdb4v",
      "tag_16",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "6omen4",
      "tag_17",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-y3fz4f",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1612405306647,
    "updatedAt": 1612405306647,
    "author": {
      "username": "author-fsdlm5",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "6omen4",
      "tag_17",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "3fzt4m",
      "tag_18",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-x8i7rk",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1612405306688,
    "updatedAt": 1612405306688,
    "author": {
      "username": "authoress-gvwrjp",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "3fzt4m",
      "tag_18",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "jt6408",
      "tag_19",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-ytatj9",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1612405306732,
    "updatedAt": 1612405306732,
    "author": {
      "username": "author-fsdlm5",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "jt6408",
      "tag_19",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
### should list articles
```
GET /articles
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "jt6408",
        "tag_19",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1612405306732,
      "author": {
        "username": "author-fsdlm5",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ytatj9",
      "updatedAt": 1612405306732,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "3fzt4m",
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1612405306688,
      "author": {
        "username": "authoress-gvwrjp",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-x8i7rk",
      "updatedAt": 1612405306688,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "6omen4",
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1612405306647,
      "author": {
        "username": "author-fsdlm5",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-y3fz4f",
      "updatedAt": 1612405306647,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "dbdb4v",
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1612405306620,
      "author": {
        "username": "authoress-gvwrjp",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ka05x6",
      "updatedAt": 1612405306620,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_15",
        "tag_mod_2_1",
        "tag_mod_3_0",
        "wlg39v"
      ],
      "createdAt": 1612405306587,
      "author": {
        "username": "author-fsdlm5",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-sfdpdq",
      "updatedAt": 1612405306587,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "lsptn9",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1612405306562,
      "author": {
        "username": "authoress-gvwrjp",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-p6jf1b",
      "updatedAt": 1612405306562,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "fdv9o2",
        "tag_13",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1612405306539,
      "author": {
        "username": "author-fsdlm5",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-jbhxbn",
      "updatedAt": 1612405306539,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0",
        "yhhefy"
      ],
      "createdAt": 1612405306513,
      "author": {
        "username": "authoress-gvwrjp",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-6tiqk1",
      "updatedAt": 1612405306513,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "s8osai",
        "tag_11",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1612405306490,
      "author": {
        "username": "author-fsdlm5",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-oqjmzy",
      "updatedAt": 1612405306490,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "kzw7ti",
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1612405306467,
      "author": {
        "username": "authoress-gvwrjp",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-t9ehkb",
      "updatedAt": 1612405306467,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "inlxwa",
        "tag_9",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1612405306441,
      "author": {
        "username": "author-fsdlm5",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-1q5lz9",
      "updatedAt": 1612405306441,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "ljg2t7",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1612405306410,
      "author": {
        "username": "authoress-gvwrjp",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-g4ewyg",
      "updatedAt": 1612405306410,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_7",
        "tag_mod_2_1",
        "tag_mod_3_1",
        "y9aezi"
      ],
      "createdAt": 1612405306378,
      "author": {
        "username": "author-fsdlm5",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-f93syh",
      "updatedAt": 1612405306378,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0",
        "y20oky"
      ],
      "createdAt": 1612405306352,
      "author": {
        "username": "authoress-gvwrjp",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-q46fax",
      "updatedAt": 1612405306352,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "9dy7tg",
        "tag_5",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1612405306327,
      "author": {
        "username": "author-fsdlm5",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-mqatk",
      "updatedAt": 1612405306327,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tafj9g",
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1612405306302,
      "author": {
        "username": "authoress-gvwrjp",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-srtkro",
      "updatedAt": 1612405306302,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "p6wgj7",
        "tag_3",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1612405306275,
      "author": {
        "username": "author-fsdlm5",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-89c206",
      "updatedAt": 1612405306275,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "q2c37m",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1612405306249,
      "author": {
        "username": "authoress-gvwrjp",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ks960d",
      "updatedAt": 1612405306249,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "gwibbd",
        "tag_1",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1612405306217,
      "author": {
        "username": "author-fsdlm5",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-lvdap4",
      "updatedAt": 1612405306217,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0",
        "ufkf2m"
      ],
      "createdAt": 1612405306157,
      "author": {
        "username": "authoress-gvwrjp",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-p9sh4v",
      "updatedAt": 1612405306157,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should list articles with tag
```
GET /articles?tag=tag_7
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "tag_7",
        "tag_mod_2_1",
        "tag_mod_3_1",
        "y9aezi"
      ],
      "createdAt": 1612405306378,
      "author": {
        "username": "author-fsdlm5",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-f93syh",
      "updatedAt": 1612405306378,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
```
GET /articles?tag=tag_mod_3_2
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "6omen4",
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1612405306647,
      "author": {
        "username": "author-fsdlm5",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-y3fz4f",
      "updatedAt": 1612405306647,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "lsptn9",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1612405306562,
      "author": {
        "username": "authoress-gvwrjp",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-p6jf1b",
      "updatedAt": 1612405306562,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "s8osai",
        "tag_11",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1612405306490,
      "author": {
        "username": "author-fsdlm5",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-oqjmzy",
      "updatedAt": 1612405306490,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "ljg2t7",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1612405306410,
      "author": {
        "username": "authoress-gvwrjp",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-g4ewyg",
      "updatedAt": 1612405306410,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "9dy7tg",
        "tag_5",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1612405306327,
      "author": {
        "username": "author-fsdlm5",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-mqatk",
      "updatedAt": 1612405306327,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "q2c37m",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1612405306249,
      "author": {
        "username": "authoress-gvwrjp",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ks960d",
      "updatedAt": 1612405306249,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should list articles by author
```
GET /articles?author=authoress-gvwrjp
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "3fzt4m",
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1612405306688,
      "author": {
        "username": "authoress-gvwrjp",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-x8i7rk",
      "updatedAt": 1612405306688,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "dbdb4v",
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1612405306620,
      "author": {
        "username": "authoress-gvwrjp",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ka05x6",
      "updatedAt": 1612405306620,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "lsptn9",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1612405306562,
      "author": {
        "username": "authoress-gvwrjp",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-p6jf1b",
      "updatedAt": 1612405306562,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0",
        "yhhefy"
      ],
      "createdAt": 1612405306513,
      "author": {
        "username": "authoress-gvwrjp",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-6tiqk1",
      "updatedAt": 1612405306513,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "kzw7ti",
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1612405306467,
      "author": {
        "username": "authoress-gvwrjp",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-t9ehkb",
      "updatedAt": 1612405306467,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "ljg2t7",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1612405306410,
      "author": {
        "username": "authoress-gvwrjp",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-g4ewyg",
      "updatedAt": 1612405306410,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0",
        "y20oky"
      ],
      "createdAt": 1612405306352,
      "author": {
        "username": "authoress-gvwrjp",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-q46fax",
      "updatedAt": 1612405306352,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tafj9g",
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1612405306302,
      "author": {
        "username": "authoress-gvwrjp",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-srtkro",
      "updatedAt": 1612405306302,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "q2c37m",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1612405306249,
      "author": {
        "username": "authoress-gvwrjp",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ks960d",
      "updatedAt": 1612405306249,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0",
        "ufkf2m"
      ],
      "createdAt": 1612405306157,
      "author": {
        "username": "authoress-gvwrjp",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-p9sh4v",
      "updatedAt": 1612405306157,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should list articles favorited by user
```
GET /articles?favorited=non-author-1pv8u5
```
```
200 OK

{
  "articles": []
}
```
### should list articles by limit/offset
```
GET /articles?author=author-fsdlm5&limit=2
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "jt6408",
        "tag_19",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1612405306732,
      "author": {
        "username": "author-fsdlm5",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ytatj9",
      "updatedAt": 1612405306732,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "6omen4",
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1612405306647,
      "author": {
        "username": "author-fsdlm5",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-y3fz4f",
      "updatedAt": 1612405306647,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
```
GET /articles?author=author-fsdlm5&limit=2&offset=2
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "tag_15",
        "tag_mod_2_1",
        "tag_mod_3_0",
        "wlg39v"
      ],
      "createdAt": 1612405306587,
      "author": {
        "username": "author-fsdlm5",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-sfdpdq",
      "updatedAt": 1612405306587,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "fdv9o2",
        "tag_13",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1612405306539,
      "author": {
        "username": "author-fsdlm5",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-jbhxbn",
      "updatedAt": 1612405306539,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should list articles when authenticated
```
GET /articles
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "jt6408",
        "tag_19",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1612405306732,
      "author": {
        "username": "author-fsdlm5",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ytatj9",
      "updatedAt": 1612405306732,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "3fzt4m",
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1612405306688,
      "author": {
        "username": "authoress-gvwrjp",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-x8i7rk",
      "updatedAt": 1612405306688,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "6omen4",
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1612405306647,
      "author": {
        "username": "author-fsdlm5",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-y3fz4f",
      "updatedAt": 1612405306647,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "dbdb4v",
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1612405306620,
      "author": {
        "username": "authoress-gvwrjp",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ka05x6",
      "updatedAt": 1612405306620,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_15",
        "tag_mod_2_1",
        "tag_mod_3_0",
        "wlg39v"
      ],
      "createdAt": 1612405306587,
      "author": {
        "username": "author-fsdlm5",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-sfdpdq",
      "updatedAt": 1612405306587,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "lsptn9",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1612405306562,
      "author": {
        "username": "authoress-gvwrjp",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-p6jf1b",
      "updatedAt": 1612405306562,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "fdv9o2",
        "tag_13",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1612405306539,
      "author": {
        "username": "author-fsdlm5",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-jbhxbn",
      "updatedAt": 1612405306539,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0",
        "yhhefy"
      ],
      "createdAt": 1612405306513,
      "author": {
        "username": "authoress-gvwrjp",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-6tiqk1",
      "updatedAt": 1612405306513,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "s8osai",
        "tag_11",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1612405306490,
      "author": {
        "username": "author-fsdlm5",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-oqjmzy",
      "updatedAt": 1612405306490,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "kzw7ti",
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1612405306467,
      "author": {
        "username": "authoress-gvwrjp",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-t9ehkb",
      "updatedAt": 1612405306467,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "inlxwa",
        "tag_9",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1612405306441,
      "author": {
        "username": "author-fsdlm5",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-1q5lz9",
      "updatedAt": 1612405306441,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "ljg2t7",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1612405306410,
      "author": {
        "username": "authoress-gvwrjp",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-g4ewyg",
      "updatedAt": 1612405306410,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_7",
        "tag_mod_2_1",
        "tag_mod_3_1",
        "y9aezi"
      ],
      "createdAt": 1612405306378,
      "author": {
        "username": "author-fsdlm5",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-f93syh",
      "updatedAt": 1612405306378,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0",
        "y20oky"
      ],
      "createdAt": 1612405306352,
      "author": {
        "username": "authoress-gvwrjp",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-q46fax",
      "updatedAt": 1612405306352,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "9dy7tg",
        "tag_5",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1612405306327,
      "author": {
        "username": "author-fsdlm5",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-mqatk",
      "updatedAt": 1612405306327,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tafj9g",
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1612405306302,
      "author": {
        "username": "authoress-gvwrjp",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-srtkro",
      "updatedAt": 1612405306302,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "p6wgj7",
        "tag_3",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1612405306275,
      "author": {
        "username": "author-fsdlm5",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-89c206",
      "updatedAt": 1612405306275,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "q2c37m",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1612405306249,
      "author": {
        "username": "authoress-gvwrjp",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ks960d",
      "updatedAt": 1612405306249,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "gwibbd",
        "tag_1",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1612405306217,
      "author": {
        "username": "author-fsdlm5",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-lvdap4",
      "updatedAt": 1612405306217,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0",
        "ufkf2m"
      ],
      "createdAt": 1612405306157,
      "author": {
        "username": "authoress-gvwrjp",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-p9sh4v",
      "updatedAt": 1612405306157,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should disallow multiple of author/tag/favorited
```
GET /articles?tag=foo&author=bar
```
```
GET /articles?author=foo&favorited=bar
```
```
GET /articles?favorited=foo&tag=bar
```
## Feed
### should get feed
```
GET /articles/feed
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Only one of these can be specified: [tag, author, favorited]"
    ]
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Only one of these can be specified: [tag, author, favorited]"
    ]
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Only one of these can be specified: [tag, author, favorited]"
    ]
  }
}
```
```
200 OK

{
  "articles": []
}
```
```
POST /profiles/authoress-gvwrjp/follow

{}
```
```
200 OK

{
  "profile": {
    "username": "authoress-gvwrjp",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
GET /articles/feed
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "3fzt4m",
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1612405306688,
      "author": {
        "username": "authoress-gvwrjp",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-x8i7rk",
      "updatedAt": 1612405306688,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "dbdb4v",
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1612405306620,
      "author": {
        "username": "authoress-gvwrjp",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ka05x6",
      "updatedAt": 1612405306620,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "lsptn9",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1612405306562,
      "author": {
        "username": "authoress-gvwrjp",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-p6jf1b",
      "updatedAt": 1612405306562,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0",
        "yhhefy"
      ],
      "createdAt": 1612405306513,
      "author": {
        "username": "authoress-gvwrjp",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-6tiqk1",
      "updatedAt": 1612405306513,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "kzw7ti",
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1612405306467,
      "author": {
        "username": "authoress-gvwrjp",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-t9ehkb",
      "updatedAt": 1612405306467,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "ljg2t7",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1612405306410,
      "author": {
        "username": "authoress-gvwrjp",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-g4ewyg",
      "updatedAt": 1612405306410,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0",
        "y20oky"
      ],
      "createdAt": 1612405306352,
      "author": {
        "username": "authoress-gvwrjp",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-q46fax",
      "updatedAt": 1612405306352,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tafj9g",
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1612405306302,
      "author": {
        "username": "authoress-gvwrjp",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-srtkro",
      "updatedAt": 1612405306302,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "q2c37m",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1612405306249,
      "author": {
        "username": "authoress-gvwrjp",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ks960d",
      "updatedAt": 1612405306249,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0",
        "ufkf2m"
      ],
      "createdAt": 1612405306157,
      "author": {
        "username": "authoress-gvwrjp",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-p9sh4v",
      "updatedAt": 1612405306157,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
```
POST /profiles/author-fsdlm5/follow

{}
```
```
200 OK

{
  "profile": {
    "username": "author-fsdlm5",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
GET /articles/feed
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "jt6408",
        "tag_19",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1612405306732,
      "author": {
        "username": "author-fsdlm5",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ytatj9",
      "updatedAt": 1612405306732,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "3fzt4m",
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1612405306688,
      "author": {
        "username": "authoress-gvwrjp",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-x8i7rk",
      "updatedAt": 1612405306688,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "6omen4",
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1612405306647,
      "author": {
        "username": "author-fsdlm5",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-y3fz4f",
      "updatedAt": 1612405306647,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "dbdb4v",
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1612405306620,
      "author": {
        "username": "authoress-gvwrjp",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ka05x6",
      "updatedAt": 1612405306620,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_15",
        "tag_mod_2_1",
        "tag_mod_3_0",
        "wlg39v"
      ],
      "createdAt": 1612405306587,
      "author": {
        "username": "author-fsdlm5",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-sfdpdq",
      "updatedAt": 1612405306587,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "lsptn9",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1612405306562,
      "author": {
        "username": "authoress-gvwrjp",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-p6jf1b",
      "updatedAt": 1612405306562,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "fdv9o2",
        "tag_13",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1612405306539,
      "author": {
        "username": "author-fsdlm5",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-jbhxbn",
      "updatedAt": 1612405306539,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0",
        "yhhefy"
      ],
      "createdAt": 1612405306513,
      "author": {
        "username": "authoress-gvwrjp",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-6tiqk1",
      "updatedAt": 1612405306513,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "s8osai",
        "tag_11",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1612405306490,
      "author": {
        "username": "author-fsdlm5",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-oqjmzy",
      "updatedAt": 1612405306490,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "kzw7ti",
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1612405306467,
      "author": {
        "username": "authoress-gvwrjp",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-t9ehkb",
      "updatedAt": 1612405306467,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "inlxwa",
        "tag_9",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1612405306441,
      "author": {
        "username": "author-fsdlm5",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-1q5lz9",
      "updatedAt": 1612405306441,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "ljg2t7",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1612405306410,
      "author": {
        "username": "authoress-gvwrjp",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-g4ewyg",
      "updatedAt": 1612405306410,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_7",
        "tag_mod_2_1",
        "tag_mod_3_1",
        "y9aezi"
      ],
      "createdAt": 1612405306378,
      "author": {
        "username": "author-fsdlm5",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-f93syh",
      "updatedAt": 1612405306378,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0",
        "y20oky"
      ],
      "createdAt": 1612405306352,
      "author": {
        "username": "authoress-gvwrjp",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-q46fax",
      "updatedAt": 1612405306352,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "9dy7tg",
        "tag_5",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1612405306327,
      "author": {
        "username": "author-fsdlm5",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-mqatk",
      "updatedAt": 1612405306327,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tafj9g",
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1612405306302,
      "author": {
        "username": "authoress-gvwrjp",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-srtkro",
      "updatedAt": 1612405306302,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "p6wgj7",
        "tag_3",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1612405306275,
      "author": {
        "username": "author-fsdlm5",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-89c206",
      "updatedAt": 1612405306275,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "q2c37m",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1612405306249,
      "author": {
        "username": "authoress-gvwrjp",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ks960d",
      "updatedAt": 1612405306249,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "gwibbd",
        "tag_1",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1612405306217,
      "author": {
        "username": "author-fsdlm5",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-lvdap4",
      "updatedAt": 1612405306217,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0",
        "ufkf2m"
      ],
      "createdAt": 1612405306157,
      "author": {
        "username": "authoress-gvwrjp",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-p9sh4v",
      "updatedAt": 1612405306157,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should disallow unauthenticated feed
```
GET /articles/feed
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
## Tags
### should get tags
```
GET /tags
```
```
200 OK

{
  "tags": [
    "lsptn9",
    "tag_14",
    "tag_mod_2_0",
    "tag_mod_3_2",
    "s8osai",
    "tag_11",
    "tag_mod_2_1",
    "tag_6",
    "tag_mod_3_0",
    "y20oky",
    "6omen4",
    "tag_17",
    "fdv9o2",
    "tag_13",
    "tag_mod_3_1",
    "dbdb4v",
    "tag_16",
    "ljg2t7",
    "tag_8",
    "kzw7ti",
    "tag_10",
    "p6wgj7",
    "tag_3",
    "9dy7tg",
    "tag_5",
    "jt6408",
    "tag_19",
    "tafj9g",
    "tag_4",
    "q2c37m",
    "tag_2",
    "tag_0",
    "ufkf2m",
    "tag_12",
    "yhhefy",
    "3fzt4m",
    "tag_18",
    "tag_7",
    "y9aezi",
    "gwibbd",
    "tag_1",
    "tag_15",
    "wlg39v",
    "inlxwa",
    "tag_9",
    "tag_a",
    "tag_b"
  ]
}
```
# Comment
```
POST /users

{
  "user": {
    "email": "author-a5x11l@email.com",
    "username": "author-a5x11l",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "author-a5x11l@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImF1dGhvci1hNXgxMWwiLCJpYXQiOjE2MTI0MDUzMDcsImV4cCI6MTYxMjU3ODEwN30.pZ58GCgzcs_ynfm-pESwvTXWl4CN_h1mVWiy0MP7A-Y",
    "username": "author-a5x11l",
    "bio": "",
    "image": ""
  }
}
```
```
POST /users

{
  "user": {
    "email": "commenter-vk738n@email.com",
    "username": "commenter-vk738n",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "commenter-vk738n@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImNvbW1lbnRlci12azczOG4iLCJpYXQiOjE2MTI0MDUzMDgsImV4cCI6MTYxMjU3ODEwOH0.bL0LWh743sv-Dpca_R_5xl5OvUFfQA5s3v3RwPqB7aI",
    "username": "commenter-vk738n",
    "bio": "",
    "image": ""
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body"
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-iw75jt",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1612405308024,
    "updatedAt": 1612405308024,
    "author": {
      "username": "author-a5x11l",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
## Create
### should create comment
```
POST /articles/title-iw75jt/comments

{
  "comment": {
    "body": "test comment 2dvxvz"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "118fe00f-4cd7-4d79-bfa2-a12d5dea6068",
    "slug": "title-iw75jt",
    "body": "test comment 2dvxvz",
    "createdAt": 1612405308105,
    "updatedAt": 1612405308105,
    "author": {
      "username": "commenter-vk738n",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-iw75jt/comments

{
  "comment": {
    "body": "test comment at1pmn"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "87970325-bda7-4dbf-b51c-1a8e2e332b27",
    "slug": "title-iw75jt",
    "body": "test comment at1pmn",
    "createdAt": 1612405308134,
    "updatedAt": 1612405308134,
    "author": {
      "username": "commenter-vk738n",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-iw75jt/comments

{
  "comment": {
    "body": "test comment qb51ub"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "f66c424c-93ad-4185-ba2a-cd969b898d5e",
    "slug": "title-iw75jt",
    "body": "test comment qb51ub",
    "createdAt": 1612405308182,
    "updatedAt": 1612405308182,
    "author": {
      "username": "commenter-vk738n",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-iw75jt/comments

{
  "comment": {
    "body": "test comment 1kgsxp"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "f15e889d-66c3-4e20-a351-8859aa75ea9f",
    "slug": "title-iw75jt",
    "body": "test comment 1kgsxp",
    "createdAt": 1612405308224,
    "updatedAt": 1612405308224,
    "author": {
      "username": "commenter-vk738n",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-iw75jt/comments

{
  "comment": {
    "body": "test comment slgevq"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "fde892c1-4436-40ab-81b6-25288c9568ab",
    "slug": "title-iw75jt",
    "body": "test comment slgevq",
    "createdAt": 1612405308258,
    "updatedAt": 1612405308258,
    "author": {
      "username": "commenter-vk738n",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-iw75jt/comments

{
  "comment": {
    "body": "test comment -zhshia"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "474dcb4b-7e37-4ba7-bd62-a7a0bdec02db",
    "slug": "title-iw75jt",
    "body": "test comment -zhshia",
    "createdAt": 1612405308294,
    "updatedAt": 1612405308294,
    "author": {
      "username": "commenter-vk738n",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-iw75jt/comments

{
  "comment": {
    "body": "test comment 2dnrn4"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "5bb90eb4-e82a-4ed7-a517-e546ff12b8bb",
    "slug": "title-iw75jt",
    "body": "test comment 2dnrn4",
    "createdAt": 1612405308332,
    "updatedAt": 1612405308332,
    "author": {
      "username": "commenter-vk738n",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-iw75jt/comments

{
  "comment": {
    "body": "test comment ver8wd"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "6d210439-fb51-41cc-8eab-ac817ab450b6",
    "slug": "title-iw75jt",
    "body": "test comment ver8wd",
    "createdAt": 1612405308370,
    "updatedAt": 1612405308370,
    "author": {
      "username": "commenter-vk738n",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-iw75jt/comments

{
  "comment": {
    "body": "test comment 32oeju"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "c0b53340-ddb0-4f86-bc24-3d2c665cc29e",
    "slug": "title-iw75jt",
    "body": "test comment 32oeju",
    "createdAt": 1612405308422,
    "updatedAt": 1612405308422,
    "author": {
      "username": "commenter-vk738n",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-iw75jt/comments

{
  "comment": {
    "body": "test comment iuxvhj"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "b14a196d-29b2-4178-be8e-d7c4b48ff94d",
    "slug": "title-iw75jt",
    "body": "test comment iuxvhj",
    "createdAt": 1612405308458,
    "updatedAt": 1612405308458,
    "author": {
      "username": "commenter-vk738n",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
### should disallow unauthenticated user
```
POST /articles/title-iw75jt/comments

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should enforce comment body
```
POST /articles/title-iw75jt/comments

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Comment must be specified."
    ]
  }
}
```
### should disallow non-existent article
```
POST /articles/foobar/comments

{
  "comment": {
    "body": "test comment pzps72"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [foobar]"
    ]
  }
}
```
## Get
### should get all comments for article
```
GET /articles/title-iw75jt/comments
```
```
200 OK

{
  "comments": [
    {
      "createdAt": 1612405308105,
      "id": "118fe00f-4cd7-4d79-bfa2-a12d5dea6068",
      "body": "test comment 2dvxvz",
      "slug": "title-iw75jt",
      "author": {
        "username": "commenter-vk738n",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1612405308105
    },
    {
      "createdAt": 1612405308224,
      "id": "f15e889d-66c3-4e20-a351-8859aa75ea9f",
      "body": "test comment 1kgsxp",
      "slug": "title-iw75jt",
      "author": {
        "username": "commenter-vk738n",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1612405308224
    },
    {
      "createdAt": 1612405308134,
      "id": "87970325-bda7-4dbf-b51c-1a8e2e332b27",
      "body": "test comment at1pmn",
      "slug": "title-iw75jt",
      "author": {
        "username": "commenter-vk738n",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1612405308134
    },
    {
      "createdAt": 1612405308458,
      "id": "b14a196d-29b2-4178-be8e-d7c4b48ff94d",
      "body": "test comment iuxvhj",
      "slug": "title-iw75jt",
      "author": {
        "username": "commenter-vk738n",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1612405308458
    },
    {
      "createdAt": 1612405308258,
      "id": "fde892c1-4436-40ab-81b6-25288c9568ab",
      "body": "test comment slgevq",
      "slug": "title-iw75jt",
      "author": {
        "username": "commenter-vk738n",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1612405308258
    },
    {
      "createdAt": 1612405308422,
      "id": "c0b53340-ddb0-4f86-bc24-3d2c665cc29e",
      "body": "test comment 32oeju",
      "slug": "title-iw75jt",
      "author": {
        "username": "commenter-vk738n",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1612405308422
    },
    {
      "createdAt": 1612405308294,
      "id": "474dcb4b-7e37-4ba7-bd62-a7a0bdec02db",
      "body": "test comment -zhshia",
      "slug": "title-iw75jt",
      "author": {
        "username": "commenter-vk738n",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1612405308294
    },
    {
      "createdAt": 1612405308370,
      "id": "6d210439-fb51-41cc-8eab-ac817ab450b6",
      "body": "test comment ver8wd",
      "slug": "title-iw75jt",
      "author": {
        "username": "commenter-vk738n",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1612405308370
    },
    {
      "createdAt": 1612405308332,
      "id": "5bb90eb4-e82a-4ed7-a517-e546ff12b8bb",
      "body": "test comment 2dnrn4",
      "slug": "title-iw75jt",
      "author": {
        "username": "commenter-vk738n",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1612405308332
    },
    {
      "createdAt": 1612405308182,
      "id": "f66c424c-93ad-4185-ba2a-cd969b898d5e",
      "body": "test comment qb51ub",
      "slug": "title-iw75jt",
      "author": {
        "username": "commenter-vk738n",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1612405308182
    }
  ]
}
```
## Delete
### should delete comment
```
DELETE /articles/title-iw75jt/comments/118fe00f-4cd7-4d79-bfa2-a12d5dea6068
```
```
200 OK

{}
```
### only comment author should be able to delete comment
```
DELETE /articles/title-iw75jt/comments/87970325-bda7-4dbf-b51c-1a8e2e332b27
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Only comment author can delete: [commenter-vk738n]"
    ]
  }
}
```
### should disallow unauthenticated user
```
DELETE /articles/title-iw75jt/comments/87970325-bda7-4dbf-b51c-1a8e2e332b27
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should disallow deleting unknown comment
```
DELETE /articles/title-iw75jt/comments/foobar_id
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Comment ID not found: [foobar_id]"
    ]
  }
}
```
# User
## Create
### should create user
```
POST /users

{
  "user": {
    "email": "user1-0.pi1tmzctsho@email.com",
    "username": "user1-0.pi1tmzctsho",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "user1-0.pi1tmzctsho@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAucGkxdG16Y3RzaG8iLCJpYXQiOjE2MTI0MDUzMDgsImV4cCI6MTYxMjU3ODEwOH0.LUOUz2JLtDx2d4Q8IiBzyZM0V_N-4QaKCmy7mgkrcLA",
    "username": "user1-0.pi1tmzctsho",
    "bio": "",
    "image": ""
  }
}
```
### should disallow same username
```
POST /users

{
  "user": {
    "email": "user1-0.pi1tmzctsho@email.com",
    "username": "user1-0.pi1tmzctsho",
    "password": "password"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Username already taken: [user1-0.pi1tmzctsho]"
    ]
  }
}
```
### should disallow same email
```
POST /users

{
  "user": {
    "username": "user2",
    "email": "user1-0.pi1tmzctsho@email.com",
    "password": "password"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email already taken: [user1-0.pi1tmzctsho@email.com]"
    ]
  }
}
```
### should enforce required fields
```
POST /users

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "User must be specified."
    ]
  }
}
```
```
POST /users

{
  "user": {
    "foo": 1
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Username must be specified."
    ]
  }
}
```
```
POST /users

{
  "user": {
    "username": 1
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email must be specified."
    ]
  }
}
```
```
POST /users

{
  "user": {
    "username": 1,
    "email": 2
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Password must be specified."
    ]
  }
}
```
## Login
### should login
```
POST /users/login

{
  "user": {
    "email": "user1-0.pi1tmzctsho@email.com",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "user1-0.pi1tmzctsho@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAucGkxdG16Y3RzaG8iLCJpYXQiOjE2MTI0MDUzMDgsImV4cCI6MTYxMjU3ODEwOH0.LUOUz2JLtDx2d4Q8IiBzyZM0V_N-4QaKCmy7mgkrcLA",
    "username": "user1-0.pi1tmzctsho",
    "bio": "",
    "image": ""
  }
}
```
### should disallow unknown email
```
POST /users/login

{
  "user": {
    "email": "0.d0xdpympeq",
    "password": "somepassword"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email not found: [0.d0xdpympeq]"
    ]
  }
}
```
### should disallow wrong password
```
POST /users/login

{
  "user": {
    "email": "user1-0.pi1tmzctsho@email.com",
    "password": "0.236kvons4b8"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Wrong password."
    ]
  }
}
```
### should enforce required fields
```
POST /users/login

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "User must be specified."
    ]
  }
}
```
```
POST /users/login

{
  "user": {}
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email must be specified."
    ]
  }
}
```
```
POST /users/login

{
  "user": {
    "email": "someemail"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Password must be specified."
    ]
  }
}
```
## Get
### should get current user
```
GET /user
```
```
200 OK

{
  "user": {
    "email": "user1-0.pi1tmzctsho@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAucGkxdG16Y3RzaG8iLCJpYXQiOjE2MTI0MDUzMDgsImV4cCI6MTYxMjU3ODEwOH0.LUOUz2JLtDx2d4Q8IiBzyZM0V_N-4QaKCmy7mgkrcLA",
    "username": "user1-0.pi1tmzctsho",
    "bio": "",
    "image": ""
  }
}
```
### should disallow bad tokens
```
GET /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
```
GET /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
```
GET /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
```
GET /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
## Profile
### should get profile
```
GET /profiles/user1-0.pi1tmzctsho
```
```
200 OK

{
  "profile": {
    "username": "user1-0.pi1tmzctsho",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
### should disallow unknown username
```
GET /profiles/foo_0.vdrnivvms7o
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "User not found: [foo_0.vdrnivvms7o]"
    ]
  }
}
```
### should follow/unfollow user
```
POST /users

{
  "user": {
    "username": "followed_user",
    "email": "followed_user@mail.com",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "followed_user@mail.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImZvbGxvd2VkX3VzZXIiLCJpYXQiOjE2MTI0MDUzMDksImV4cCI6MTYxMjU3ODEwOX0.fpjvO5oGAJOdnbOYPFD3-rXnhtww3kdvV5NoPRJZg4s",
    "username": "followed_user",
    "bio": "",
    "image": ""
  }
}
```
```
POST /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
POST /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
GET /profiles/followed_user
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
GET /profiles/followed_user
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
```
POST /users

{
  "user": {
    "username": "user2-0.tmxrrxz4a3a",
    "email": "user2-0.tmxrrxz4a3a@mail.com",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "user2-0.tmxrrxz4a3a@mail.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIyLTAudG14cnJ4ejRhM2EiLCJpYXQiOjE2MTI0MDUzMDksImV4cCI6MTYxMjU3ODEwOX0.hIZfM0T8rY6SYqA4-G9zMTtK-wERW8OQW0xy1IvBaQo",
    "username": "user2-0.tmxrrxz4a3a",
    "bio": "",
    "image": ""
  }
}
```
```
POST /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
DELETE /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
```
DELETE /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
```
DELETE /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
### should disallow following with bad token
```
POST /profiles/followed_user/follow
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
## Update
### should update user
```
PUT /user

{
  "user": {
    "email": "updated-user1-0.pi1tmzctsho@email.com"
  }
}
```
```
200 OK

{
  "user": {
    "username": "user1-0.pi1tmzctsho",
    "email": "updated-user1-0.pi1tmzctsho@email.com",
    "image": "",
    "bio": "",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAucGkxdG16Y3RzaG8iLCJpYXQiOjE2MTI0MDUzMDgsImV4cCI6MTYxMjU3ODEwOH0.LUOUz2JLtDx2d4Q8IiBzyZM0V_N-4QaKCmy7mgkrcLA"
  }
}
```
```
PUT /user

{
  "user": {
    "password": "newpassword"
  }
}
```
```
200 OK

{
  "user": {
    "username": "user1-0.pi1tmzctsho",
    "email": "updated-user1-0.pi1tmzctsho@email.com",
    "image": "",
    "bio": "",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAucGkxdG16Y3RzaG8iLCJpYXQiOjE2MTI0MDUzMDgsImV4cCI6MTYxMjU3ODEwOH0.LUOUz2JLtDx2d4Q8IiBzyZM0V_N-4QaKCmy7mgkrcLA"
  }
}
```
```
PUT /user

{
  "user": {
    "bio": "newbio"
  }
}
```
```
200 OK

{
  "user": {
    "username": "user1-0.pi1tmzctsho",
    "bio": "newbio",
    "image": "",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAucGkxdG16Y3RzaG8iLCJpYXQiOjE2MTI0MDUzMDgsImV4cCI6MTYxMjU3ODEwOH0.LUOUz2JLtDx2d4Q8IiBzyZM0V_N-4QaKCmy7mgkrcLA"
  }
}
```
```
PUT /user

{
  "user": {
    "image": "newimage"
  }
}
```
```
200 OK

{
  "user": {
    "username": "user1-0.pi1tmzctsho",
    "image": "newimage",
    "bio": "newbio",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAucGkxdG16Y3RzaG8iLCJpYXQiOjE2MTI0MDUzMDgsImV4cCI6MTYxMjU3ODEwOH0.LUOUz2JLtDx2d4Q8IiBzyZM0V_N-4QaKCmy7mgkrcLA"
  }
}
```
### should disallow missing token/email in update
```
PUT /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
```
PUT /user

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "User must be specified."
    ]
  }
}
```
### should disallow reusing email
```
POST /users

{
  "user": {
    "email": "user2-0.z3aody3o6g@email.com",
    "username": "user2-0.z3aody3o6g",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "user2-0.z3aody3o6g@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIyLTAuejNhb2R5M282ZyIsImlhdCI6MTYxMjQwNTMwOSwiZXhwIjoxNjEyNTc4MTA5fQ.FsmaWVNXFBN9ZqSSGl1uJ4SYuVrPA6fE4GhLUIsAsUE",
    "username": "user2-0.z3aody3o6g",
    "bio": "",
    "image": ""
  }
}
```
```
PUT /user

{
  "user": {
    "email": "user2-0.z3aody3o6g@email.com"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email already taken: [user2-0.z3aody3o6g@email.com]"
    ]
  }
}
```
# Util
## Ping
### should ping
```
GET /ping
```
```
200 OK

{
  "pong": "2021-02-04T02:21:49.539Z",
  "AWS_REGION": "us-east-1",
  "DYNAMODB_NAMESPACE": "dev"
}
```
