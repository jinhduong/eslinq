# linq-fns
.NET LINQ functions for Javascript, written by TypeScript.
- ⚡ Provide `Queryable<T>`, it's reusable, also variable and use `Predicate collection` for holding query and execute later.
- 🔨 Contains almost the original .NET and some extends methods.
- 🔨 Support `Promise` like as a input source.
- 🙅 All `APIs` like a Javascript native methods so easily, simply implementation.
- 📊 Includes some simple drivers. (like as `firebase real db`) 

```js
npm install linq-fns --save
```

> This version just alpha so if have any problem, don't hesitate to let me know. 👋

### Basic exampl
#### Node or browser
```ts
// ES6
import { Queryable } from 'linq-fns';

// ES5
const Queryable = require('linq-fns').Queryable;

let query = Queryable
            .from(nations)
            .join(continents, (x, y) => x.areaId === y.id)
            .groupBy(o => o.y.areaName)
            .select(x => {
                return {
                    area: x.key,
                    total: Queryable.fromSync(x.items).count() // Here will return number, not Promise<number>
                }
            })
const asyncData = query.toList() // Will return Promise<{area:string, total:number}>
asyncData.then(data => {
    console.log(data);
    // [
    //     {area: 'Euro': total: 2},
    //     {area:'South Ameria', total: 1}
    // ]
});
```

#### Firebase
``` ts
const FireBaseQueryale = require('linq-fns').FireBaseQueryale;
const admin = require('firebase-admin');
const serviceAccount = require('./serviceAccountKey');

admin.initializeApp({
    credential: admin.credential.cert(serviceAccount),
    databaseURL: 'https://xxx.firebaseio.com'
});

const db = admin.database();
const postsQuery = new FireBaseQueryale(db,'<yourdb>.posts');

// READ AND QUERY DATA
// ES5 Promise
postsQuery.getQuery().where('...').select('...').toList().then(x=>'...');

// Async/await
const data = await postsQuery.getQuery().where('...').select('...').toList();

// WRITE DATA
// Just call not execute to server
postsQuery.add(item);
postsQuery.remove(item);
postsQuery.update(item);

// Call this to execute 3 above methods
postsQuery.commitChanges();

```

### Process
#### 1.Methods
- [x] from
- [x] where
- [x] select
- [x] selectMany
- [x] join
- [x] leftJoin
- [x] groupJoin
- [x] orderBy
- [x] orderByDescending
- [x] take
- [x] takeWhile
- [x] skip
- [x] skipWhile
- [x] groupBy
- [x] distinct
- [x] concat
- [x] zip
- [x] union
- [x] intersect
- [x] except
- [x] first : `Promise<T>`
- [x] firstOrDefault : `Promise<T | null>`
- [x] last : `Promise<T>`
- [x] lastOrDefault : `Promise<T | null>`
- [x] single
- [x] singleOrDefault
- [x] contains
- [x] sequenceEqual
- [x] any : `Promise<boolean>`
- [x] all : `Promise<boolean>`
- [x] count : `Promise<number>`
- [x] min : `Promise<number>`
- [x] max : `Promise<number>`
- [x] sum : `Promise<number>`
- [x] average
- [x] aggregate
- [x] toList : `Promise<T[]>`

#### 2. Drivers
- [x] Firebase
- [ ] Localstorage
- [ ] Gists Github
- [ ] ...

### License

[MIT License](http://opensource.org/licenses/MIT)
