# Neo4j Browser

## Development setup

1.  Clone this repo
1.  Install yarn globally (not required but recommended): `npm install -g yarn`
1.  Install project dependencies: `yarn`

### Development server

`yarn start` and point your web browser to `http://localhost:8080`.

### Testing

`yarn test` to run a single test run. A linter will run first.

`yarn dev` to have continuous testing on every file change.

#### E2E Suite

`yarn e2e` to run the cypress js test suite (requires a fresh installation of neo4j to run against, expects neo4j 3.4 by default).
`yarn e2e --env server=3.3` to only run cypress js tests valid for neo4j server version 3.3.

To run on an existing server (with a password already set), you can use any of these (the default password is set to "newpassword", pass in `--env browser-password=your-password`):  
`yarn e2e-local --end server=3.4`  
`yarn e2e-local-open --end server=3.4`  
The latter just opens Cypress runner so you can see the tests being executed and run only some of them. Very useful when writing tests.

There are also e2e tests that covers import from CSV files. To run thise, copy the `e2e_tests/files/import.csv` to the `import/` directory of the database you want to run the tests on and then start the e2e tests with the `--env include-import-tests=true` flag.
Example: `yarn e2e-local-open --env server=3.4,include-import-tests=true`

Here are the available options / env variables:

```
server=3.2|3.3|3.4|3.5 (default 3.4)
browser-password=<your-pw> (default 'newpassword')
include-import-tests=true|false (default false)
bolt-url=<bolt url excluding the protocol> (default localhost:7687)
```

Test environment options (cannot be set using the `--env` flag as the ones above).
These needs to be set before the test command is run.

```
CYPRESS_E2E_TEST_ENV=local|null (if the initial set of pw should run or not) (default undefined)
CYPRESS_BASE_URL=<url to reach the browser to test> (default http://localhost:8080)
```

Example: `CYPRESS_E2E_TEST_ENV="local" CYPRESS_BASE_URL=http://localhost:8081 cypress open --env server=3.4`

## Devtools

Download these two chrome extensions:

- [Redux devtools](https://chrome.google.com/webstore/detail/redux-devtools/lmhkpmbekcpmknklioeibfkpmmfibljd?hl=en)
- [React devtools](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi?hl=en)

## Images

Create node property called `image_url` and populate this with a fully qualified image url.


```
MATCH (n:MyImageNode)
SET n.image_url = "http://myimage.png"
RETURN n
```

smaller images (100x100 px) work better, use the largest node size (80px) for best effect.

## Neo4j Desktop

Update Neo4j Desktop, copy and paste the npm repo link (below) in the 'Install Graph Application' box, and then add Neo4j Browser Images app to your Project.

https://registry.npmjs.org/neo4j-browser-image-enabled

<img width="299" alt="graph-app-url" src="https://user-images.githubusercontent.com/5991751/50950037-878a1b80-145d-11e9-900e-4949b78af427.png">
