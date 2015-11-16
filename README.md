# Testing LinkLocal with NPM 3.X

**Disclaimer: it is pretty clear that local packages are NOT the best solution, publish your packages somewhere if you can!**

There are two apps that share local packages.  The first, `app1`, only depends on `package1` directly and has a lodash module that is shared.  The second relies on both `package1`, `package2` and the shared lodash module.  Lastly, `package1` depends on `package2`, so we can see nested dependencies.

To run this youself just clone the repo and run `npm start`.

Here is what you end up with after running the link command found in the package.json:

```
app1/
  node_modules/
    lodash.defaults/
	# ... And all of lodash.defaults deps
    package1/ -> ../packages/package1/
    package2/
  index.js
  package.json

app2/
  node_modules/
    lodash.defaults/
	# ... And all of lodash.defaults deps
    package1/ -> ../packages/package1/
    package2/ -> ../packages/package2/
  index.js
  package.json

packages/

  package1/
    node_modules/
      lodash.defaults/
	  # ... And all of lodash.defaults deps
      package2/ -> ../package2/
    index.js
    package.json

  package2/
    node_modules/
	  # ... And all of lodash.defaults deps
      lodash.defaults/
    index.js
    package.json
```
