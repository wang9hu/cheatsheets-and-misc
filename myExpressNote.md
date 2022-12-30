Express is a backend framekwork in Nodejs.

- fast, un-opinionated, and minimal
- flexible and scalable
- mostly used
- no more listening for stream events
- tons of useful methods

```
router.post('/newdog', (req, res) => {
  req.body.name
  ....
  return res.status(200).json(res.locals.newDog)
})
```

req.body:

- for POST or PUT request, when sending data to server
- use express.json() parse incoming body

req.params

- usually in patch and delete method
- properies attached to the url as end router point (.../:prop)

req.query

- greate for sorting, pagination, filtering
- `/something?age=senior&size=small`

middleware:

```
agg.get('/', **function1, function2, function3**, (req, res) => {
  // send response here
})
```

use next() inside of middleware:

- to chain middleware
- with asynchronous function
- `res.locals` object: move throught middleware chain and taking variable inside to the next middleware
- will trigger global error handler if `next(err)` is invoked
  <br>

express check from top to bottom:

- if `app.use('/')` is before `app.use('/something')`, the second will never run
  <br>
- use`app.use(express.json())` to handle parsing request body, put it at top before handling others
  <br>

request: `'.../api/characters/3'`

- `app.use('.../api/', route)`
  - `route('.../characters', (req. res) => {}):` will run
  - `route('.../characters/:id', (req, res) => {}) : req.params.id = 3`
