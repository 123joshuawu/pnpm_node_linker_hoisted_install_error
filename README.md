
Summary:

`.npmrc` contains the following configuration:
```
shared-workspace-lockfile=false
node-linker=hoisted
```

`pnpm-workspace.yaml` setup with
```
packages:
  - 'apps/*'
```

One workspace `apps/test` with the following dependencies:
```
    "dependencies": {
      "typeorm": "^0.3.16"
    },
    "devDependencies": {
      "@types/node": "^20.2.3",
      "ts-node": "^10.9.1",
      "typescript": "^5.0.4"
    }
```

Command `pnpm install --prod` fails for latest v6 and v7:

![pnpm v6](https://github.com/123joshuawu/pnpm_node_linker_hoisted_install_error/actions/workflows/pnpm_v6.yaml/badge.svg)

Install error in version 6: `ERR_PNPM_LOCKFILE_MISSING_DEPENDENCY  Broken lockfile: no entry for '/ts-node/10.9.1_6e60fac3ec6053710c20ba789de9afc7' in pnpm-lock.yaml`


![pnpm v7](https://github.com/123joshuawu/pnpm_node_linker_hoisted_install_error/actions/workflows/pnpm_v7.yaml/badge.svg)

Install error in version 7:
`ERR_PNPM_MISSING_HOISTED_LOCATIONS  /@jridgewell/resolve-uri/3.1.1 is not found in hoistedLocations inside node_modules/.modules.yaml`


The issue in both versions seems to be related with `ts-node` being an optional peer dependency of `typeorm` but not sure of the root cause.
