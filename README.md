# Go Bitcask Storage Engine

A Go implementation of the bitcask storage engine (https://riak.com/assets/bitcask-intro.pdf) used in Riak KV

## Implementation 
Bitcask is a log-structured hash table for fast key/value data. Similar to LSM Trees, Bitcask keeps log files of all 
datafiles and performs merging when needed to reduce read latency. Bitcask's advantages come from it's in-memory key directory, which caches the file\_id of each key, such that every read only requires at most one disk seek.

## Usage
From the root directory, run

```bash
mkdir datastore
go build ./...
go run ./cmd
```

## API
```
db := bitcask.Open("new-bitcask-store", bitcask.READ|bitcask.WRITE|bitcask.CREATE)
err := db.Put("key", "value")
value, err := db.Get("key")
db.Delete("key")
db.Put("another key", "another value")
db.Merge()
db.Get("another key")
```
