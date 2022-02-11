# microservice.comments
Microservice to handle simple comment-systems


```
GET  /:project/comments/:post                                      // list all comments by post
POST /:project/comments/:post?token=$hash&hook.data.anchor=season01e01          // create a new comment to a post
PUT/GET  /:project/comments/:post/:id/confirm/?data.emailConfirmed=true&token.emailConfirmed=$hash  // confirm a commenters mail-address
```



### `identifier`
18 character identifier 

### Auth-Structure
```
{
  auth; {
    type: ['GET', 'PUT'],
    path: '…'
  }
  data: {
    emailConfirmed: true,
  },
  actions: [{
    type: 'redirect',
    url: 'https://parser.signalwerk.ch/#confirm'
  }],
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

### Webhook-Structure

```
add.comment: `https://mail.signalwerk.ch/parser/comments/confirm/
```
gets data: 

```
{
  hook: {
    data: {
      // additional data
    }
  },
  data: {
    // data from db
  }
}
```





