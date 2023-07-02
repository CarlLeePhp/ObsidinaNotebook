This is the back end for the project 2.

## Dependencies

```npm init -y```

Then change main becomes "server.js"

```npm i express bcryptjs jsonwebtoken config express-validator mongoose```

**jsonwebtoken:** An implementation of JSON Web Tokens.

**config:** Configure your Node.js Application ( https://www.npmjs.com/package/config );

```npm i -D nodemon concurrently```

**nodemon:** automatically reload the application when something changed. A script could be added ```"server": "nodemon server.js"```.

**concurrently:** used for running back-end and front-end applications at the same time.



## Changes of package.json

```json
{
    "scripts":{
        "start": "node server.js",
        "server": "nodemon server.js"
    }
}
```



## Basic Server.js

```javascript
const express = require('express');

const app = express();

const PORT = process.env.PORT || 5000;

app.listen(PORT, () => 	console.log(`Server started on port ${PORT}`));
```



## Connect Database (MongoDB)

A config file can be used to store the information of the database ```config/db.js```.

```javascript
const mongoose = require('mongoose');
const config = require('config');
const db = config.get('mongoURI');

const connectDB = async () => {
    try {
        await mongoose.connect(db, {
            useNewUrlParser: true,
            useCreateIndex: true,
            useFindAndModify: false
        });
        console.log('MongoDB Connected...')
    } catch (err){
        console.error("Error:" + err.message);
        process.exit(1);
    }
};

module.exports = connectDB;
```

**config/default.json** mongoURI from Database service supplier.

```json
{
    "mongoURI": "mongodb+srv://..."
}
```

In the server.js

```javascript
const express = require('express');
const connectDB = require('./config/db');

const app = express();

// Connect Database
connectDB();
```



## Express Testing

```javascript
const express = require('express');

const app = express();

const PORT = process.env.PORT || 5000;

app.listen(PORT, () => console.log(`Server started on port ${PORT}`));
```



## Router

server.js

```javascript
// Define Routes
app.use('/api/users', require('./routes/users'));
app.use('/api/auth', require('./routes/auth'));
app.use('/api/contacts', require('./routes/contacts'));
```

users.js (simplest)

```javascript
const express = require('express');
const router = express.Router();

// @route    POST api/users
// @desc     Register a user
// @access   Public
router.post('/',(req, res) => {
    res.send("This is users router");
});

module.exports = router;
```

