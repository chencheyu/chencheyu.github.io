---
date: 2024-02-18
publish: true
slug: a3067e81-81a5-407d-84a9-ede6e971d6ea
tags:
- CS/Backend
title: Cherrypy Cookie
---
# cherrypy cookie

### 概述

他是用python的simple cookie，所以Morsel屬性該有的多有(屬性要小寫)，但她不能刪除只能設程過期

### Cookie 設定

```python
cherrypy.response.cookie[key] = value #設質  
cherrypy.response.cookie[key]["max-age"] = 60*60*8 #有效期8小時
```

### Cookie 讀取

```python
cie = cherrypy.request.cookie.keys() #取得所有cookie  
uid = cherrypy.request.cookie["uid"].value
```

設定跟讀取在不同物件上  
在cherrypy 18.5 上測試
