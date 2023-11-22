## Reproduction attempt

For https://github.com/prisma/prisma/issues/21471

Make sure to have a database running and edit the `.env` file.

```sh
# Check your Node.js version
node -v

yarn

docker compose up -d

yarn prisma db push

NODE_OPTIONS="--max-old-space-size=200" yarn ts-node main.ts
```


### Results, from running on a Codespace (Ubuntu)
- Prisma `5.3.1`
- Node.js `v18.16.0` (the user didn’t specify which v18)
- a JSON of 1MB

Short analysis: no memory leak detected, rss and head are stable over time.
```
rss (MiB),heapTotal (MiB),heapUsed (MiB),external (MiB),arrayBuffers (MiB)
259.9,143.0,106.1,7.957,4.127,
323.6,144.3,106.8,21.29,5.126,
322.2,144.6,106.6,21.29,5.126,
319.7,144.3,106.8,21.29,5.126,
319.7,144.6,106.7,21.29,5.126,
323.8,141.6,104.1,24.29,4.126,
321.2,141.6,104.2,24.29,4.126,
318.7,141.9,104.2,24.29,4.126,
316.2,141.6,104.1,24.29,4.126,
315.9,141.9,104.1,24.29,4.126,
315.5,141.6,104.1,24.29,4.126,
327.1,141.9,104.2,24.29,4.126,
329.5,141.9,104.2,24.29,4.126,
329.5,141.6,104.1,24.29,4.126,
330.0,141.9,104.2,24.29,4.126,
330.0,141.9,104.1,24.29,4.126,
329.8,141.6,104.1,24.29,4.126,
329.7,141.6,104.1,24.29,4.126,
330.0,141.9,104.1,24.29,4.126,
329.9,141.6,104.4,24.29,4.126,
330.2,141.9,104.1,24.29,4.126,
330.1,141.9,104.1,24.29,4.126,
330.1,141.9,104.1,24.29,4.126,
330.1,141.9,104.3,24.29,4.126,
331.2,141.9,104.4,24.29,4.126,
331.3,141.9,104.1,24.29,4.126,
331.4,141.9,104.2,24.29,4.126,
331.6,142.1,104.1,24.29,4.126,
331.3,141.9,104.1,24.29,4.126,
331.2,141.6,104.2,24.29,4.126,
331.2,141.6,104.1,24.29,4.126,
331.2,141.9,104.2,24.29,4.126,
331.2,141.9,104.2,24.29,4.126,
331.3,141.9,104.2,24.29,4.126,
331.4,141.9,104.2,24.29,4.126,
331.2,141.9,104.4,24.29,4.126,
331.4,141.9,104.3,24.29,4.126,
331.4,141.9,104.3,24.29,4.126,
331.3,141.9,104.2,24.29,4.126,
331.4,141.9,104.4,24.29,4.126,
331.5,141.9,104.2,24.29,4.126,
331.4,141.9,104.2,24.29,4.126,
331.5,142.1,104.2,24.29,4.126,
```