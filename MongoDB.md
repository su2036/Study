## 1. DataBase
### 1-1. 생성
> `use DB명` = 생성, 기존 DB가 있는 경우 해당 DB를 사용한다는 명령.

### 1-2. 조회
> `show dbs` = DB List 확인
> `db` = 현재 사용중인 DB 확인
> `db.stats()` = DB 상태확인

### 1-3. 제거
> `db.dropDatabase()` = 현재 위치가 삭제하려는 DB를 use로 사용하는 상태에서 실행해야되는 명령어

```ex) > use testdb  > (testdb)> db.dropDatabase()```



## 2. Collection (=mysql에서 Table과 동일)
### 2-1. 생성
> `db.createCollection(name, [optinons])` = 컬렉션 생성, name은 컬랙션이름/options은 document 타입
- Options 객체의 속성
- capped : Boolean타입, 이 값을 true로 설정하면, capped collection을 활성화 시킴.
Capped collection이란 고정된 크기(fixed size)를 가진 컬렉션으로서, size가 초과되면 가장 오래된 데이터를 덮어씀. 이 값을 true로 설정하면 size값을 꼭 설정 해야함.

- autoindex :Boolean타입, 이 값을 true로 설정하면, _id 필드에 index를 자동 생성함. 기본값은 false 

- size :number타입, capped collection을 위해 해당 컬렉션의 최대 사이즈를 ~bytes로 지정 

- max : number타입
```
ex) > db.createCollection("test", {
capped : true,
size : 6142800,
max : 10000
})
결과:{"ok" : 1}
```
 
### 2-2. 조회
> `show collections` = 컬렉션 리스트를 확인

### 2-3. 제거
> `db.컬렉션명.drop()` = 해당 컬렉션 삭제

### 2-4. 유틸(컬렉션명 변경)
> `db.기존컬렉션명.renameCollection("newCollectionName") 


## 3. Document
### 3-1. 생성
> `db.컬렉션명.insert(document) = document추가, 배열형식으로 전달하면 여러 document를 bulk형식으로 추가 가능
```ex)> db.books.insert([
{"language": "java", "level": 5},
{"language": "ruby", "framework": "rails"}
]);
BulkWriteResult({
"writeErrors" : [ ],
"writeConcernErrors" : [ ],
"nInserted" : 2,
"nUpserted" : 0,
"nMatched" : 0,
"nModified" : 0,
"nRemoved" : 0,
"upserted" : [ ]
})
```

### 3-2. 조회
> `db.컬렉션명.find([query, projection])` = 해당 컬렉션의 document 리스트를 확인 + `.pretty()` 정렬
> `db.컬렉션명.find().pretty()`
