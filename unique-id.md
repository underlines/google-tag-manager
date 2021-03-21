# NanoID for small UUIDv4 compliant unique ID generation
If you need to generate a unique id, you should not use Math.random() or Date.now(), as these have a high chance of collision. This is related to the birthday paradox.
To have a much lower probability of collision, but still maintain high performance and small size for your Google Tag Manager container, you can use nanoid.

## Implementation
Use the following snipped in a CUstom HTML Tag or Custom Javascript Variable:
```
//naoid
let nanoid=(t=21)=>{let e="",r=crypto.getRandomValues(new Uint8Array(t));for(;t--;){let n=63&r[t];e+=n<36?n.toString(36):n<62?(n-26).toString(36).toUpperCase():n<63?"_":"-"}return e};
dataLayer.push({
  event : 'UniqueId',
  nanoid : nanoid(8)
});
```
* You can change the length in `nanoid(8)`, to any other number.

Another example for a Custom Javascript Variable that returns the ID:
```
function(
  let nanoid=(t=21)=>{let e="",r=crypto.getRandomValues(new Uint8Array(t));for(;t--;){let n=63&r[t];e+=n<36?n.toString(36):n<62?(n-26).toString(36).toUpperCase():n<63?"_":"-"}return e};
  return nanoid(10);
);
```

