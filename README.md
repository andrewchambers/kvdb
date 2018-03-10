# kvdb

A key value database for the command line, writes and reads are atomic, ordered and safe in the event of power loss. 

The database is just an sqlite3 file, requires python3.

The database allows concurrent readers, but a writing process will cause all others to wait up 5 seconds to aquire a lock, aborting with a non zero error code on timeout.

The default database is ./kv.db, get exits with code 111 if a key does not exist.

Help strings:

```
$ kvdb --help
usage: kvdb [-h] [--db DB] {get,del,set} ...

Simple key value store using sqlite3.

positional arguments:
  {get,del,set}

optional arguments:
  -h, --help     show this help message and exit
  --db DB        database file
```

```
$ kvdb set --help
usage: kvdb set [-h] [-f] set_key set_value

positional arguments:
  set_key
  set_value

optional arguments:
  -h, --help  show this help message and exit
  -f          read the file at path set_value as the value

```

```
$ kvdb get --help
usage: kvdb get [-h] [-n] get_key

positional arguments:
  get_key

optional arguments:
  -h, --help  show this help message and exit
  -n          don't print a new line after the value

```

```
$ kvdb del --help
usage: kvdb del [-h] del_key

positional arguments:
  del_key

optional arguments:
  -h, --help  show this help message and exit
```


Example usage:
```
$ kvdb get foo
$ echo $?
111
$ kvdb set foo bar
$ kvdb get foo
bar
$ kvdb del foo
```
