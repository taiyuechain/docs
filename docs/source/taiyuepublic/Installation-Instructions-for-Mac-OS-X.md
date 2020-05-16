## Building from source

### Building  (command line client)

Clone the repository to a directory of your choosing:

```shell
git clone Taipublic
```

Building `getrue` requires the Go compiler:

```shell
brew install go
```

Finally, build the `getrue` program using the following command.
```shell
cd truechain-engineering-code
git checkout release/2.0
make getrue
```

If you see some errors related to header files of Mac OS system library, install XCode Command Line Tools, and try again.

```shell
xcode-select --install
```

You can now run `build/bin/getrue` to start your node.
