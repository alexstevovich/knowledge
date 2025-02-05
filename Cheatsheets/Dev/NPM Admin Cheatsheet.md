Login 

``` bat
npm login
```

if successful
Logged in as <your-username> on https://registry.npmjs.org/.

# Versioning

``` bat
npm version patch   # For small bug fixes
npm version minor   # For new features
npm version major   # For breaking changes
```

## Beta Version

``` bat
npm version 1.0.0-beta.1
```

you can increment anything you want even the number after the beta

tags it in npm as beta

``` bat
npm publish --tag beta
```

## GitError when publishing
You can't update version when git changes aren't staged so you have to add and commit first.

# Publishing

First publish:

```
npm publish --access public
```
If successful, you'll see:
 + package-name@1.0.0
  

 Verify Your Package on NPM
 https://www.npmjs.com/package/<package-name> 


## Unpubilsh
You can unpublish before 72 hours or 100 downloads (As of the time of writing this). The package name will be made reavailable if you unpublished the initial publish.

``` bat
npm unpublish --force
```

# Global Install

you can install with
 ```
 npm install package-name
 ```