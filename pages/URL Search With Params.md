tags:: URL, Javascript, typescript
```javascript
let u = new URL("http://localhost/")

const monate = ["august", "märz"]

monate.forEach(monat => {u.searchParams.append("monat", monat)})

u.toString()
```

-
-