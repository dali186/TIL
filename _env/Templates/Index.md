```dataview
table description as "한줄소개", dateformat(file.ctime,"yyyy-MM-dd HH:mm:ss") as "최초작성일자", dateformat(file.mtime,"yyyy-MM-dd HH:mm:ss") as "최종수정일자"
from ""
where file.name != "Index"
```
-- from을 경로로 변경