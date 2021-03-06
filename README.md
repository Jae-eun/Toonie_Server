# Toonie API
투니서버와 투니 앱클라이언트 사이에 쓰이는 API
RESTFull API로, JSON 형식으로 데이터를 주고 받는다.

## API list
1. App Vesion API
2. Token API
3. Keyword API
4. Tag API
5. Toon API
6. Work List API
7. My Keyword API

------- 

## App Version API
APP 버전 정보를 조회하는 API로 GET METHOD만 지원하고, 이 API를 호출함으로서, 업데이트되어야 하는 Vesion 정보를 확인 할 수 있다.

### METHODE : GET 
#### URL : /appversion

#### Request
```
    N/A(보내지 않음)
```

#### Response
| KEY | VALUE |
| :-----: | ------: |
| succces | API 호출 성공 여부 |
| foreUpdateYn | 강제 업데이트 여부 |
| limitVersion | 업데이트가 필요한 버전정보(이 버전 이하로는 업데이트 필요 |
| updateMessage | 업데이트 메세지 |
| updateRedirectURL | 업데이트 Redirect URL |

```
    {
        "success" : "success",
        "foreUpdateYn" : "Y",
        "limitVersion" : "1.0.0",
        "updateMessage" : "현재 사용할 수 없는 버전입니다."
        "updateRedirectURL" : "www.itunes.com/istore/.."
    }
```

-------

## Token API
APP 사용자를 구분하기 위한 Token 값을 발급받기 위한 API로 발급 받은 Token을 APP에 저장하여 사용

### METHODE : GET
#### URL : /token

#### Request
```
    N/A(보내지 않음)
```

#### Response
| KEY | VALUE |
| :-----: | ------: |
| succees | API 호출 성공 여부 |
| token | 토큰값(12자리) |


```
    {
        "success" : "success",
        "token" : "190307000001"
    }
```

### Token 생성 규칙
12자리 숫자로 생성하며, yymmdd!@#$%^로 구성하며, !@#$%^는 000001부터 순차적으로 증가시킨다.

-----------
## Keyword API
키워드를 조회/입력/삭제할 수 있는 API

### METHODE : GET
#### URL : /kewords
전체 키워드 리스트를 조회

#### Request 
```
    N/A(보내지 않음)
```

#### Response
| KEY | VALUE |
| :-----: | ------: |
| succees | API 호출 성공 여부 |
| keywords | 키워드들의 배열 |

```
    {
        "success" : "success",
        "keywords" : [ "키워드1", "키워드2", "키워드3", ... ]
    }
```


### METHOD : POST
#### URL : /keywords
키워드 정보(키워드-태그에 포함된 인스타툰)을 등록할 수 있는 API

#### Request
| KEY | VALUE |
| :-----: | ------: |
| keyword | 관심 키워드 |
| tag | 태그 |
| toonIDs | 인스타툰 ID 배열 |

```
    {
        "keyword" : "동물",
        "tag" : "귀여운"
        "toonIDs" : [ "웰시코시 일기", "멍뭉이 일기", "냥이 일기",...]
    }
```

keyword, tag, toonID가 하나의 Primary Key로 묶임

#### Response
| KEY | VALUE |
| :-----: | ------: |
| succees | API 호출 성공 여부 |

```
    {
        "success" : "success"
    }
```

### METHOD : GET
#### URL : /keywords/:token
해당 사용자가 등록한 관심키워드에 속한 태그와 웹툰 정보를 조회

통쾌한을 데이터 값으로 설정해서 보내라 "tag" : "통쾌한"

#### Request

```
    N/A
```

#### Response
| KEY | VALUE |
| :-----: | ------: |
| succees | API 호출 성공 여부 |
| tags | 검색한 키워드에 속한 태그-툰 정보|

```
{
 success : success,
 tags : [
            { 
             통쾌한 : [
                           { 
                             toonID : 1235,
                             toonName : 신의탑,
                             instaID : sinetop,
                             instaURL : www.instagram.com/sietop,
                             thumbnail : wwww.instagram.com/sietop/dsdsad
                           },
                           { 
                             toonID : 1234,
                             toonName : 신의탑2,
                             instaID : sinetop,
                             instaURL : www.instagram.com/sietop,
                             thumbnail : wwww.instagram.com/sietop/dsdsad
                           }
                         ]
             },
            고양이 : [
                           { 
                             toonID : 1236,
                             toonName : 야옹,
                             instaID : yaya,
                             instaURL : www.instagram.com/yaya,
                             thumbnail : wwww.instagram.com/yaya/dsdsad
                           },
                           {
                             toonID : 1237,
                             toonName : 나비,
                             instaID : navi,
                             instaURL : www.instagram.com/navi,
                             thumbnail : wwww.instagram.com/navi/dsdsad
                           }
                         ]
             }
         
}
```

#### toonID
작가의 인스타 ID로 할려고 했으나, 인스타 ID는 바뀔 수 있는 부분이라 투니에서 주어진 고유의 ID를 사용할 예정


### METHOD : DELETE
#### URL : /keywords
키워드 정보(키워드-태그에 포함된 인스타툰)을 삭제할 수 있는 API

#### Request 
| KEY | VALUE |
| :-----: | ------: |
| keyword | 관심 키워드 |
| tag | 태그 |
| toonIDs | 인스타툰 ID 배열 |

```
    {
        "keyword" : "동물",
        "tag" : "귀여운"
        "toonIDs" : [ "웰시코시 일기",  "멍뭉이 일기"]
    }
```


#### Response
| KEY | VALUE |
| :-----: | ------: |
| success | API 호출 성 여부 |

```
    {
        "success" : "success"
    }
```

-------------

## Tag API
태그 정보를 조회할 수 있는 API


### METHOD : GET
#### URL : /tags
전체 태그 리스트를 조회하는 API

#### Request
```
    N/A
```

#### Response
| KEY | VALUE |
| :-----: | ------: |
| success | API 호출 성 여부 |
| tags | 태그 배열 |

```
    {
        "success" : "success"
        "tags" : ["태그1", "태그2", ...]
    }
```

### METHOD : GET
#### URL : /tags/:tag
태그를 포함한 키워드와 태그에 속한 웹툰 정보를 조회하는 API

#### Request
```
    N/A
```

#### Response

| KEY | VALUE |
| :-----: | ------: |
| success | API 호출 성 여부 |
| keywords | 태그를 포함한 키워드 배열 |
| toons | 태그에 속한 웹툰 정보 배열 |

```
    {
        "success" : "success",
        "keywords" : ["키워드1", "키워드2", "키워드3"...],
        "toons" : [
                    { 
                    toonID : 1236,
                    toonName : 야옹,
                    instaID : yaya,
                    instaURL : www.instagram.com/yaya,
                    thumbnail : wwww.instagram.com/yaya/dsdsad
                    },
                    {
                    toonID : 1237,
                    toonName : 나비,
                    instaID : navi,
                    instaURL : www.instagram.com/navi,
                    thumbnail : wwww.instagram.com/navi/dsdsad
                    }
                ]
    }
```

---------------

## Toon API
인스타툰 정보를 가져올 수 있는 API

### METHOD : GET
#### URL : /toons
전체 인스타툰 리스트를 조회하는 API

#### Request
```
    N/A
```

#### Response
| KEY | VALUE |
| :-----: | ------: |
| success | API 호출 성 여부 |
| toons | 인스타툰 정보 배열|

```
    {
        "success" : "success",
         "toons" : [
                    { 
                        toonID : 1236,
                        toonName : 야옹,
                        instaID : yaya,
                        instaURL : www.instagram.com/yaya,
                        thumbnail : wwww.instagram.com/yaya/dsdsad
                    },
                    {
                        toonID : 1237,
                        toonName : 나비,
                        instaID : navi,
                        instaURL : www.instagram.com/navi,
                        thumbnail : wwww.instagram.com/navi/dsdsad
                    },
                    ...
                ]
    }
```

### METHOD : GET
#### URL : /toon/:toonID
특정 인스타툰 정보를 조회하는 API

#### Request
```
    N/A
```

#### Response
| KEY | VALUE |
| :-----: | ------: |
| success | API 호출 성 여부 |
| toonID | 인스타툰 ID|
| toonName | 인스타툰 이름 |
| instaID | 작가인스타 ID |
| insetURL | 인스타툰 URL |
| thumbNail| 인스타툰 썸네일 이미지 |

```
    {
        "success" : "success",
        "toonID" : "1237",
        "toonName" : "나비",
        "instaID" : "navi",
        "instaURL" : "www.instagram.com/navi",
        "thumbnail" : "wwww.instagram.com/navi/dsdsad"
    }
```


-----------

## Work List API
작품목록(북마크)을 조회/생성/삭제할 수 있는 API

### METHOD : GET
#### URL : /worklist/:token
해당 사용자의 작품목록(북마크) 정보를 불러오는 API

#### Request
```
    N/A
```

#### Response
| KEY | VALUE |
| :-----: | ------: |
| success | API 호출 성 여부 |
| workList | 작품목록 정보  |

```
    {
        "success" : "success",
        "workList" : [
            {
                "workListName" : "전체작품목록",
                "workListinfo" : "전체",
                "workList : [
                   {
                       "toonID" : "1235",
                       "regDate" : "20190306152130",
                       "orderNo" : 0
                    },
                   {
                       "toonID" : "1237",
                       "regDate" : "20190307123321",
                       "orderNo" : 1
                   } 
                ]
            },
            {
                "workListName" : "종강은 언제?",
                "workListinfo" : "인생 종강은 언제일까요? 교수님",
                "workList : [
                   {
                       "toonID" : "1235",
                       "regDate" : "20190306152130",
                       "orderNo" : 0
                    },
                   {
                       "toonID" : "1237",
                       "regDate" : "20190307123321",
                       "orderNo" : 1
                   } 
                ]
            }
        ]
    }
```

### MEHTOD : POST
#### URL : /worklist
작품목록을 생성 또는 수정하는 API

#### Request
| KEY | VALUE |
| :-----: | ------: |
| token | token 값 |
| workList | 작품목록 정보 |

```
    {
        "token" : "190307123456",
        "workListName" : "종강은 언제?",
        "workListinfo" : "인생 종강은 언제일까요? 교수님",
        "workList : [
           {
               "toonID" : "1235",
               "regDate" : "20190306152130",
               "state" : "DELETE"
               "orderNo" : 0
            },
           {
               "toonID" : "1237",
               "regDate" : "20190307123321"
               "state" : "ADD"
               "orderNo" : 1
           } 
        ]
    }
```

#### Response

```
    {
        "success" : "success"
    }
```
### MEHTOD : DELETE
#### URL : /worklist
생성된 작품목록을 삭제하는 API

#### Request
| KEY | VALUE |
| :-----: | ------: |
| token | token 값 |
| workListName | 작품목록 이름 |

```
    {
        "token" : "190307123456",
        "workListName" : "종강은 언제?"
    }
```

#### Response

```
    {
        "success" : "success"
    }
```


## My KeyWord API

### METHOD : GET
#### URL : /mykeywords/:token
해당 사용자가 관심키워드로 등록한 키워드를 조회하는 API

#### Request
```
    N/A
```
#### Response
```
    {
        "success" : "success",
        "myKeywords" : ["키워드1", "키워드2", "키워드3", ...]
    }
```

### METHOD : POST
#### URL : /mykeywords
해당 사용자가 관심키워드를 등록 또는 삭제할 수 있는 API
state 없이 매번 새로운 리스트 전달

#### Request
```
    {
        "token" : "190303123456",
        "myKeywords" : [
            {
                "keyword" : "키워드4",
                "state" : "ADD" 
            },
            {
                "keyword" : "키워드1",
                "state" : "DELETE" 
            }
        ]
    }
```


#### Response
```
    {
        "success" : "success"
    }
```




데이터 보내서 있으면 DELETE, 없으면 INSERT

