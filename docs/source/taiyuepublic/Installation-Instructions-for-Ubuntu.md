## Building from source

### Building taipublic (command line client)

Clone the repository to a directory of your choosing:

```shell
git clone github.com/taiyuechain/taipublicchain
```



Install latest distribution of [Go](https://golang.org/) if you don't have it already.

Building `taipublic` requires Go and C compilers to be installed:

```shell
sudo apt-get install -y build-essential
```

Checkout the lasted release branch: 
```shell
cd taipublicchain
git checkout release/2.0
```

Finally, build the `taipublic` program using the following command.
```shell
make taipublic
```

You can now run `build/bin/taipublic` to start your node.