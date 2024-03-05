This repo demonstrates an issue with the `@nx/next:build` executor when the child process is killed via SIGKILL or SIGTERM. This can happen when CI terminates a process when using up too much resources.

Issue: https://github.com/nrwl/nx/issues/22148

Run:

```
npx nx sigkill
```
