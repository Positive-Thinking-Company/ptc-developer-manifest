# Dependencies for Node.js


## Check for new versions
If using **yarn**:
`yarn upgrade-interactive --latest`

If using **npm** only:
`npm outdated`
or the recommended package from nestjs website:

`npm install -g npm-check-updates`
`ncu`

Examples of usage to check for *@nestjs* prefixed packages:
```cmd
ncu @nestjs*
ncu "/^@nestjs.*$/"
```

## Check for unused dependencies

Be careful, dependencies that are used by scripts are shown (so don't delete everything before doing a search on the project).

`npx depcheck`

## See dependency graph

Sometimes it's useful to see what dependencies are bound to internal (inferred) dependencies.
To view that graph in npm, type: `npm ls -a`
