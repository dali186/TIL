---
published: <% tp.date.now('YYYY-MM-DD HH:mm:ss') %>
lastModified: <% tp.file.last_modified_date('YYYY-MM-DD HH:mm:ss') %>
path: <% tp.file.folder(true) %>
category: 
description: <% tp.system.prompt('문서 설명') %>
tags:
---
