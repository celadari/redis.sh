# redis_sh
Basic Redis client, written in Bash allowing to read/write keys and sets in redis database from bash commands.

It is an extension of [redi.sh](https://github.com/crypt1d/redi.sh) which allows reading/writing hashes.

## Usage:

> By default redi.sh reads input from stdin and interprets it as a variable or an array (if -a is used) or a hash (if -h is used).
>To avoid setting redis hostname and port number with each command, you can export REDIS_HOST and REDIS_PORT variables.

```
./redi.sh [-a] [-g <variable|array>] [-p <password>] [-H <hostname>] [-P <port>]

    -a              : Tells the script that we are working with arrays, instead of regular variables.
    -h              : Tells the script that we are working with hashes, instead of regular variables.
    -r <min,max>    : When used with -a, defines the range of elements to get from the array. Default is all (0,-1).
    -g <name>       : Get the variable/array specified by <name> and output it to stdout.
    -s <name>       : Set the variable/array specified by <name> with the input from stdin.
    -f <name>       : Set the hash field specified by <name> with the input from stdin.
    -p <password>   : Use "AUTH <password>" before running the SET/GET command to authenticate to redis.
    -H <hostname>   : Specify a custom hostname to connect to. Default is localhost.
    -d <number>     : Specify a custom database number from range 0-15\. Default is 0
    -P <port>       : Specify a custom port to connect to. Default is 6379.
    -w <name>       : Deletes specified key from database
    -W              : Deletes all keys (same as '-w *')
```

## Example:
```shell
$ echo "banane" | ./redi.sh -hs john -f favorite_fruit
$ ./redi.sh -hg john -f favorite_fruit
banane
```

```shell
$ echo "banane" | ./redi.sh -hs john -f favorite_fruit
$ echo "red" | ./redi.sh -hs john -f favorite_color
$ ./redi.sh -hg john
banane
red
```

```shell
$ echo "this is a variable" | ./redi.sh -s testvar
$ ./redi.sh -g testvar
this is a variable
```

```shell
$ echo red green blue | ./redi.sh -as Colors
$ ./redi.sh -ag Colors
red
green
blue
```

## License

MIT