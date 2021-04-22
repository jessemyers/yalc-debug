# yalc-debug

Reproduces a behavior difference between `yalc` and `yarn pack`.


## Baseline

The baseline behavior is assumed to be that of `yarn pack`:

```sh
$ yarn --version
1.22.10

$ yarn build

$ yarn pack

$ tar tvzf yalc-debug-v1.0.0.tgz
drwxr-xr-x  0 0      0           0 Apr 22 11:45 package
-rw-r--r--  0 0      0        1068 Apr 22 11:33 package/LICENSE
-rw-r--r--  0 0      0          12 Apr 22 11:33 package/README.md
drwxr-xr-x  0 0      0           0 Apr 22 11:45 package/dist
-rw-r--r--  0 0      0         384 Apr 22 11:45 package/package.json
-rw-r--r--  0 0      0          19 Apr 22 11:45 package/dist/index.js
-rw-r--r--  0 0      0         384 Apr 22 11:45 package/dist/package.json
```

## Behavior with 1.0.0-pre.50

```sh
$ yalc --version
1.0.0-pre.50

$ yalc publish --files
Files included in published content:
- LICENSE
- dist/package.json
- package.json
- README.md
Total 4 files.
yalc-debug@1.0.0+51b035e3 published in store.
```

Notice that `dist/index.js` is absent. The difference of behavior seems to depend on whether
`package.json` is included in the `dist` (build) output.
