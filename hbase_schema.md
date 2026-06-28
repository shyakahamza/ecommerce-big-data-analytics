\# HBase Schema — E-Commerce Analytics



\## Setup Instructions



\### 1. Start HBase (Docker)

```bash

docker start hbase-local

docker exec -d hbase-local hbase thrift start

```



\### 2. Open HBase Shell

```bash

docker exec -it hbase-local hbase shell

```



\### 3. Create Tables



\#### Table 1: user\_sessions

Row Key Design: `user\_id\_reversetimestamp`

Example: `user\_000042\_98765432109876`



```ruby

create 'user\_sessions',

&#x20; {NAME => 'session\_info', VERSIONS => 1},

&#x20; {NAME => 'device', VERSIONS => 1},

&#x20; {NAME => 'geo', VERSIONS => 1},

&#x20; {NAME => 'activity', VERSIONS => 1}

```



\#### Table 2: product\_metrics

Row Key Design: `product\_id\_date`

Example: `prod\_00123\_2025-03-12`



```ruby

create 'product\_metrics',

&#x20; {NAME => 'stats', VERSIONS => 1},

&#x20; {NAME => 'inventory', VERSIONS => 1}

```



\### 4. Verify Tables

```ruby

list

```



\### 5. Query Examples



\#### Get all sessions for a specific user

```ruby

scan 'user\_sessions', {ROWPREFIXFILTER => 'user\_000001\_', LIMIT => 5}

```



\#### Get most recent session for a user

```ruby

scan 'user\_sessions', {ROWPREFIXFILTER => 'user\_000001\_', LIMIT => 1}

```



\#### Count total sessions loaded

```ruby

count 'user\_sessions'

```



\#### Get product metrics for a specific product

```ruby

scan 'product\_metrics', {ROWPREFIXFILTER => 'prod\_00001\_', LIMIT => 5}

```

