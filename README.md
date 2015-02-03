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
        Name string `db:"name"`  // 後面與 db 欄位的對應註釋建議加上
    }

> * Name 會對應到 tt table 的 name 欄位
> * struct 裡的 Name 或 NAME 都可以, 不分大小寫
> * struct 裡的欄位首位字母一定要大寫, 而 table 的欄位名稱都可以小寫沒有關係

### Select

    _, err := dbmap.Select(&existent_video, "select * from videos where source_website = :source_website and file_name = :file_name", map[string]interface{}{"source_website": video.Source_website, "file_name": video.File_name})
