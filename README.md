# tsbuildinfo-no-rebuild
Repro of a bug in typescript 3.4-RC

This is fixed in typescript 3.4.0-dev.20190327.

Repro:
1. `yarn` to install dependencies
2. `yarn build` to build; compilation succeeds, and a tsconfig.tsbuildinfo file is created
3. Replace the `42` in `src/example.ts` with `"hello"`
4. Run `yarn build`; it succeeds when it shouldn't
5. `rm tsconfig.tsbuildinfo`
6. Run `yarn build` to get a valid error message
7. Revert the source file to contain `42` again
8. Run `yarn build`; it still fails, with a mismatched error message:

```
$ tsc
src/example.ts:2:3 - error TS2322: Type '"hello"' is not assignable to type 'number'.

2   return 42;
    ~~~~~~~~~~
3 }
  ~
4



Found 1 error.
```
