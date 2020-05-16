## Building from source

### Building taipublic (command line client)

Clone the repository to a directory of your choosing:

```shell
git clone https://github.com/taiyuechain/taipublicchain
```
Install latest distribution of [Go](https://golang.org/) if you don't have it already.

BuilGettaipublictattaipublico and C compilers to be installed:

```shell
yum install -y build-essential
```

Finally, build the `taipublic` program using the following command.
```shell
cd truechain-engineering-code
git checkout release/2.0
make taipublic
```

You can now run `build/bin/taipublic` to start your node.