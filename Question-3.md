The JS file below has a few errors, can you indentify and fix them?

```js
const express = require(express);
const bodyParser = require('body-parser');
const mongoose = require('mongoose');
const http = require('http');

/**
 * Assume that these are error free.
 */
const User = require('./models/user');
const logger = require('./utils/logger');

const mongoDB = process.env.MONGO_URI;

const app = express();

mongoose.connect(mongoDB, { useMongoClient: true });
mongoose.Promise = global.Promise;

const db = mongoose.connection;

app.use(bodyParser.json());

// handler to save user
app.get('/save', function(res, req) {
  const user = new User(user);

  user.save(function(err) {
    if (err) {
      res.status(500).send(err);
      return logger.log(err);
    }
  });

  res.status(200).send({success: 'success', user}); 

  //return res.json(user); 
  //3. .send() above set the header Content-Type: text/plain,
  //trying to set a header (Content-Type: application/json) on a request that has already been sent will result in an Error being thrown.
});

const server = http.createServer(app);

server.listen(80, function() {
  db.on('error', function(error) {
    logger.log(error);
  });
});
```
