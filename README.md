# storage-s3

`storage-s3` 是 `storage` 模块的 `s3` 驱动。

## 安装

```bash
go get github.com/infrago/storage@latest
go get github.com/infrago/storage-s3@latest
```

## 接入

```go
import (
    _ "github.com/infrago/storage"
    _ "github.com/infrago/storage-s3"
    "github.com/infrago/infra"
)

func main() {
    infra.Run()
}
```

## 配置示例

```toml
[storage]
driver = "s3"
```

## 公开 API（摘自源码）

- `func Driver() storage.Driver`
- `func (d *s3Driver) Connect(instance *storage.Instance) (storage.Connection, error)`
- `func (c *s3Connection) Open() error`
- `func (c *s3Connection) Health() storage.Health`
- `func (c *s3Connection) Close() error`
- `func (c *s3Connection) Upload(original string, opt storage.UploadOption) (*storage.File, error)`
- `func (c *s3Connection) Fetch(file *storage.File, opt storage.FetchOption) (storage.Stream, error)`
- `func (c *s3Connection) Download(file *storage.File, opt storage.DownloadOption) (string, error)`
- `func (c *s3Connection) Remove(file *storage.File, _ storage.RemoveOption) error`
- `func (c *s3Connection) Browse(file *storage.File, opt storage.BrowseOption) (string, error)`
- `func (t *tempStream) Read(p []byte) (int, error)`
- `func (t *tempStream) Seek(offset int64, whence int) (int64, error)`
- `func (t *tempStream) ReadAt(p []byte, off int64) (int, error)`
- `func (t *tempStream) Close() error`

## 排错

- driver 未生效：确认模块段 `driver` 值与驱动名一致
- 连接失败：检查 endpoint/host/port/鉴权配置
