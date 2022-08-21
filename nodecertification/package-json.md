# Package.json

Your project's *package.json* is the central place to configure and describe how to interact with and run your application.

- https://heynode.com/tutorial/what-packagejson/ (common fields etc)

```bash
$ npm init # create initial package.json file
$ npm install <package> # install package
$ npm uninstall <package> # remove / uninstall package
$ npm update <package> # update package

$ npm install # install all package on dependencies and devdependencies

$ npm install # update all package on dependencies and devdependencies
```

- https://docs.npmjs.com/cli/v8/configuring-npm/package-json

## Semantic Versioning

```
MAJOR.MINOR.PATCH
```

- https://heynode.com/tutorial/how-use-semantic-versioning-npm/

### `^` caret

Example `^2.88.0`. The caret specifies we can update to any version greater than `2.88.0` within this major version. In the above example, the major version is 2. Anything `> 2.88.0` and `< 3.0.0` is valid. However, the caret behavior changes when a package version is still below `1.0.0`.

### Lock version numbers

When there is a *package-lock.json* file present, `npm` will install the exact same dependency tree as what's described by the *package-lock.json*. 
