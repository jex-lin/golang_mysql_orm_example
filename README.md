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

### SelectOne

    var existent_video Video
    err = dbmap.SelectOne(&existent_video, "select * from videos where source_website = :source_website and file_name = :file_name", map[string]interface{}{"source_website": video.Source_website, "file_name": video.File_name})
    // 結果 : existent_video = {1 "text"}

### Get

    qq, _ := dbmap.Get(Video{}, 1)
    // 結果 : qq = &{1 "text"}

### Update

先從 SelectOne 或 Get 拿到 struct (注意 Select 與 Get 結果是不一樣的, 差了 `&` 在前面)

    update_video := &existent_video             // 這邊加上 `&`
    update_video.Image_url = video.Image_url
    update_video.Video_url = video.Video_url
    update_video.Source_viewer = video.Source_viewer
    update_video.Updated_at = time.Now().Format("2006-01-02 15:04:05")
    update_video.File_name = video.File_name
    _, err := dbmap.Update(update_video)
    if err != nil {
        return err
    }
