# Main issue

This repo demonstrates an issue with the `@nx/next:build` executor when the child process is killed via SIGKILL or SIGTERM. This can happen when CI terminates a process when using up too much resources.

Issue: https://github.com/nrwl/nx/issues/22148

Run:

```
npx nx sigkill
```

## Another issue:

If you SIGKILL or SIGTERM the `next build` task, it will cache the task even though it did not succeed. Subsequent builds will be cached, but the output `.next` folder is missing.

Reprod:

```
# Run this, then Ctrl+C the process before it finishes
npx nx next-build

# Run it again
npxn nx next-build
```

Expected: 

The first task is not cached

Actual:

The build is read from cache, but there are no artifacts.

```
npx nx next-build

> nx run foo:next-build  [existing outputs match the cache, left as is]

   ▲ Next.js 14.0.4

   Creating an optimized production build  ..
——————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————

 NX   Successfully ran target next-build for project foo (69ms)

Nx read the output from the cache instead of running the command for 1 out of 1 tasks.
```
