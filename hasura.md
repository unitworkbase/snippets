# JWT claims


## Auth0 Rule example
```js
function hasuraClaimsRule(user, context, callback) {
  const namespace = "https://hasura.io/jwt/claims";

  context.accessToken[namespace] = {
    "x-hasura-default-role": "user",

    // do some custom logic to decide allowed roles

    "x-hasura-allowed-roles": ["user"],
    "x-hasura-user-id": user.user_id
  };
  
  callback(null, user, context);
}
```

## Auth0 User Sync Rule example
```js
function userSyncRule(user, context, callback) {
  const userId = user.user_id;
  const nickname = user.nickname;

  const mutation = `mutation($userId: String!, $nickname: String) {
    insert_users(objects: [{
        auth0_id: $userId,
        name: $nickname
      }],
      on_conflict: {
        constraint: users_pkey,
        update_columns: [name]
      }) {
        affected_rows
      }
    }`;

  request.post(
    {
      headers: {
        "content-type": "application/json",
        "x-hasura-admin-secret": configuration.HASURA_ACCESS_KEY
      },
      url: configuration.HASURA_ENDPOINT,
      body: JSON.stringify({ query: mutation, variables: { userId, nickname } })
    },
    function(error, response, body) {
      console.log(body);
      callback(null, user, context);
    }
  );
}
```
