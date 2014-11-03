# Install Mercurial

    sudo apt-get install mercurial meld

# Install mysql-server and golang-mysql driver

    sudo apt-get install mysql-server
    go get github.com/go-sql-driver/mysql
    go get github.com/coopernurse/gorp

# Create mysql data for testing

    CREATE DATABASE go_test
    CREATE TABLE tt (name char(10));

# Execute `go run main.go`

# Note

struct 對應 Table field :

    type Tt struct {
        Name string
    }

> Name 會對應到 tt table 的 name 欄位
> struct 裡的 Name 或 NAME 都可以, 不分大小寫
