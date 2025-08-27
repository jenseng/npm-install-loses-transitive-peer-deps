this repo demonstrates a bug in npm >11.5.0 around transitive peer dependencies when using workspaces

given npm >11.5.0:

if you run `npm install`, it will fail because esbuild's postinstall script won't be able to find
its expected peer dependencies (it will find the hoisted version, which is wrong), i.e. you'll get
`Error: Expected "0.21.5" but got "0.18.20"`

if you run `npm install --ignore-scripts`, it will "succeed", but the lockfile will be modified,
and rollup and esbuild's platform-specific optional peer dependencies will be missing
