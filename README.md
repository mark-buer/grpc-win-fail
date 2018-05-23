# Demo of cross-platform build failure

Packaging of certain native modules for windows using the electron-builder docker image will be unsuccessful.

electron-builder does not set the `target_libc` option when cross building for windows on linux.
This causes node-pre-gyp to use `glibc` for the `libc` `package_name` template variable.
Thus, any attempt to package a native module which uses node-pre-gyp and which specifies a `package_name` containing said `libc` variable will fail.

See https://github.com/mapbox/node-pre-gyp/issues/383 for more context.

This repo demonstates the failure by requiring the "firebase" module as a dependency ("firebase" depends upon "grpc-node" which contains a native module).

To reproduce the failure:
1. clone this repo
1. `./x-build-win`
1. observe the error message "Tried to download(403): https://storage.googleapis.com/grpc-precompiled-binaries/node/grpc/v1.11.3/electron-v2.0-win32-x64-glibc.tar.gz" and note the "-glibc" present in the name (it is supposed to be "-unknown").

This repo was derived from the...

# electron-webpack-quick-start
> A bare minimum project structure to get started developing with [`electron-webpack`](https://github.com/electron-userland/electron-webpack).

Thanks to the power of `electron-webpack` this template comes packed with...

* Use of [`webpack-dev-server`](https://github.com/webpack/webpack-dev-server) for development
* HMR for both `renderer` and `main` processes
* Use of [`babel-preset-env`](https://github.com/babel/babel-preset-env) that is automatically configured based on your `electron` version
* Use of [`electron-builder`](https://github.com/electron-userland/electron-builder) to package and build a distributable electron application

Make sure to check out [`electron-webpack`'s documentation](https://webpack.electron.build/) for more details.

## Getting Started
Simply clone down this reposity, install dependencies, and get started on your application.

The use of the [yarn](https://yarnpkg.com/) package manager is **strongly** recommended, as opposed to using `npm`.

```bash
# create a directory of your choice, and copy template using curl
mkdir new-electron-webpack-project && cd new-electron-webpack-project
curl -fsSL https://github.com/electron-userland/electron-webpack-quick-start/archive/master.tar.gz | tar -xz --strip-components 1

# or copy template using git clone
git clone https://github.com/electron-userland/electron-webpack-quick-start.git
cd electron-webpack-quick-start
rm -rf .git

# install dependencies
yarn
```

### Development Scripts

```bash
# run application in development mode
yarn dev

# compile source code and create webpack output
yarn compile

# `yarn compile` & create build with electron-builder
yarn dist

# `yarn compile` & create unpacked build with electron-builder
yarn dist:dir
```
