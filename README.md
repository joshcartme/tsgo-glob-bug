The root `tsconfig.json` works with both `tsc` and `tsgo`.

`lib/core/tsconfig.json` produces an error with `tsgo` and not with `tsc`.:

tsc:

```
$ yarn run tsc --project lib/core/tsconfig.json
yarn run v1.22.22
$ /home/repro/development/tsgo-glob-bug/node_modules/.bin/tsc --project lib/core/tsconfig.json
Done in 0.59s.
```

tsgo:

```
$ yarn run tsgo --project lib/core/tsconfig.json
yarn run v1.22.22
$ /home/repro/development/tsgo-glob-bug/node_modules/.bin/tsgo --project lib/core/tsconfig.json
lib/core/index.ts:1:14 - error TS2304: Cannot find name '$FixMe'.

1 const fixMe: $FixMe = '';
               ~~~~~~

Found 1 error in lib/core/index.ts:1
```

Changing `"../../ambient-types/**/*"` to `"../../ambient-types/*"` in `lib/core/tsconfig.json` fixes this.
