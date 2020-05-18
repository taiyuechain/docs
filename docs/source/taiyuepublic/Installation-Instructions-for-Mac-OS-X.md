## Building from source

### Building  (command line client)

Clone the repository to a directory of your choosing:

```shell
git clone https://github.com/taiyuechain/taipublicchain.git
```

Building `taipublic` requires the Go compiler:

```shell
brew install go
```

Finally, build the `taipublic` program using the following command.
```shell
cd taiyuechain/taipublicchain
git checkout master
make taipublic
```

If you see some errors related to header files of Mac OS system library, install XCode Command Line Tools, and try again.

```shell
xcode-select --install
```

You can now run `build/bin/taipublic` to start your node.
