# passport-streamlabs

[Passport](http://passportjs.org/) strategy for authenticating with [Streamlabs](https://streamlabs.com) on Node.js apps.

## Installation
`$ npm install passport-streamlabs --save`

## Usage
### Configure Strategy
1. [Register an app](https://streamlabs.com/dashboard/#/apps/register) on Streamlabs.
2. Decide what [scopes](https://twitchalerts.readme.io/docs/scopes) you're gonna use.
3. Register the strategy
```js
var StreamlabsStrategy = require('passport-streamlabs').Strategy,
    passport           = require('passport');

passport.use(new StreamlabsStrategy({
    clientID:     'YOUR_CLIENT_ID',
    clientSecret: 'YOUR_CLIENT_SECRET',
    scope:        'SCOPES', // e.g., 'donations.read donations.create' or ['donations.read', 'donations.create']
    callbackURL:  'YOUR_REDIRECT_URI'
}, function(accessToken, refreshToken, profile, done) {
    return done(undefined, profile);
}));
```

### Authenticate requests
```js
app.get('/auth/streamlabs/authorize', passport.authenticate('streamlabs'));

app.get('/auth/streamlabs/callback', passport.authenticate('streamlabs', { failureRedirect: '/auth/streamlabs/authorize' }), function(req, res) {
    // At this point, the authentication was successful.
});
```
