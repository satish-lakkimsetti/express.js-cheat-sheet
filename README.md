## Express.js Cheat Sheet

### Setup
```bash
npm init -y
npm install express
```

### Basic Server
```js
const express = require('express');
const app = express();
const PORT = 3000;

app.get('/', (req, res) => res.send('Hello World'));

app.listen(PORT, () => console.log(`Server running on port ${PORT}`));
```

### Routing
```js
app.get('/route', handler);
app.post('/route', handler);
app.put('/route/:id', handler);
app.delete('/route/:id', handler);
```

### Middleware
```js
app.use(express.json());
app.use(express.urlencoded({ extended: true }));
app.use((req, res, next) => {
  console.log(`${req.method} ${req.url}`);
  next();
});
```

### Authentication (JWT Example)
```js
const jwt = require('jsonwebtoken');

function auth(req, res, next) {
  const token = req.header('Authorization')?.split(' ')[1];
  if (!token) return res.sendStatus(401);
  try {
    req.user = jwt.verify(token, 'secret');
    next();
  } catch {
    res.sendStatus(403);
  }
}
```

### Static Files
```js
app.use(express.static('public'));
```

### Router
```js
const router = express.Router();

router.get('/', (req, res) => res.send('Router Home'));
app.use('/api', router);
```

### Error Handling
```js
app.use((err, req, res, next) => {
  console.error(err.stack);
  res.status(500).send('Something broke');
});
```

---
