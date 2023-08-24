# Dependencies for Node.js


## Check for new versions
If using **yarn**:
`yarn upgrade-interactive --latest`

If using **npm** only:
`npm outdated`
or the recommended package from nestjs website:

```cmd
npm install -g npm-check-updates
```

Then run:
```cmd
ncu
``````

Examples of usage to check for *@nestjs* prefixed packages:
```cmd
ncu "/nestjs/"
ncu @nestjs*
ncu "/^@nestjs.*$/"
```

For some specific cases where you don't want to get the latest version, for example:
```json
"@types/node": "^16.18.38"
```
update the package.json so it begins with the version you desire:
```json
"@types/node": "^18.0.0"
```
then run 
```cmd
ncu "/node/" --target minor
```
It will automatically update the package.json for you for the dependencies containing node.

## Check for unused dependencies

Be careful, dependencies that are used by scripts are shown (so don't delete everything before doing a search on the project).

`npx depcheck`

## See dependency graph

Sometimes it's useful to see what dependencies are bound to internal (inferred) dependencies.
To view that graph in npm, type: `npm ls -a`
