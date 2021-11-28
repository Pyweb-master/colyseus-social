
## Features

- Authenticate with Facebook
- Get list of user's friends
- Get list of user's online friends
- Friend requests (send, accept, decline)
- Block user

## Hooks

```typescript
import { hooks } from "@colyseus/social";

hooks.beforeAuthenticate((provider, $setOnInsert, $set) => {
    // assign default metadata upon registration
    $setOnInsert = {
        metadata: {
            coins: 100,
            trophies: 0
        }
    };
});

hooks.beforeUserUpdate((_id, fields) => {
    if (fields['username']) {
        if (fields['username'] === "bad word!") {
            throw new Error("can't have bad words!");
        }
    }
})
```

## Authentication Providers

- Anonymous
- Facebook
- _...more coming soonish!_

## Environment Variables

- `MONGO_URI`: MongoDB connection URI
- `JWT_SECRET`: Secure secret string for authentication.

### For Facebook:

- `FACEBOOK_APP_TOKEN`: Facebook App Token (`"appid|appsecret"`)

### For Push Notifications

- `WEBPUSH_SUBJECT` - mailto: or URL.
- `WEBPUSH_PUBLIC_KEY` - VAPID Public Key
- `WEBPUSH_PRIVATE_KEY` - VAPID Private Key

You can generate VAIPD keys using `npx web-push generate-vapid-keys`

## Integration with your Node.js Web Framework

### Express

```typescript
import express from "express";
import socialRoutes from "@colyseus/social/express"

const app = express();
app.use("/", socialRoutes);

app.listen(8080);
```

## TODO's

- Friend request notification (https://github.com/appfeel/node-pushnotifications)
    - On mobile
    - In the browser

## License

MIT License.
