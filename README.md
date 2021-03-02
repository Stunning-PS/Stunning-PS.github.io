
# Stunning PS 팀블로그

### 글 작성하는 법

1. `_post/` 폴더 아래 본인 이름의 폴더에 들어가 `YYYY-MM-DD-(제목).md` 의 파일을 생성한다
2. 마크다운 문서를 작성하기에 앞서, 해당 파일의 첫부분에 아래와 같이 작성해준다. 

```
---
title : # 타이틀
tags : # 태그
layout : # 레이아웃 형식. 여러가지가 있는데 article 쓰는거 추천!
author : # 본인 이름. 띄어쓰기와 대소문자 주의 (_data/authors.yml 파일에 있는 이름 참고)
date : # 해당 날짜. YYYY-MM-DD HH:MM 형식으로 작성.
---
```

커버 이미지를 포함하려면 

```
---
article_header:
  type: cover
  image:
    src: # 이미지 url 넣기
---
```

부분 추가해주기


### 글 PR하는 방법

