# microservice.comments
Microservice to handle simple comment-systems


```
GET  /:project/comments/:post                                      // list all comments by post
POST /:project/comments/:post?token=$hash                          // create a new comment to a post
PUT  /:project/comments/:post/:id/confirm/?data.emailConfirmed=true&token.emailConfirmed=$hash  // confirm a commenters mail-address
```



### `identifier`
18 character identifier 

### Auth-Structure
```
{
  data: {
    emailConfirmed: true,
  },
  token: {
    $all: [{
      field: [:admintToken]
      hash: $hash
    }],
    emailConfirmed: [{
      fields: [:secret, :datapath, :project, :post, :id, :value]
      hash: $hash
    }],
  },
}
```


