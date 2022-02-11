# seoulauction-api
seoulauction-api

## 경매 조회 API

### [POST] lots

경매 번호에 매핑된 경매 작품번호의 정보를 조회합니다.



##### 제공되는 경매 작품 정보

* **`lotNumber`** : 랏 번호
* **`lotPrice`** : 현재 가격
* **`lotTotalPrice`** : 수수료포함 가격(+19.8%) 
* **`lotStatus`** : 랏 진행 상태 (FROM_DT , TO_DT)
  * READY : 경매 시작전
  * PROGRESS : 경매중
  * FINISH : 경매 종료
  * CANCEL : 출품 취소
* **`lotBidCount`** : 경매 응찰 건수 
* **`lotEstimatePrice`**: 추정가 (by collectors 는 추정가 있음)
  * from
  * to



### 요청 예시

```sh
$ curl -XPOST http://seoulauction-api.com/lots
{
	"saleNumber": 123,
	"lotNumbers": [
		100001,
		100002,
		100003,
		100004
	]
}
```

* **`saleNumber`** : 경매 번호 (필수값)

* **`lotNumbers`** : 경매 작품 번호 (필수값)



##### 상세 설명

* 경매 정보 조회 API 는 1초 간격으로 캐쉬 값이 갱신이 됩니다. 
* 즉, 1초 이내 동일정보 호출시 동일한 값이 확인 됩니다.



### 응답 예시

```json
{
    "saleNo": 123,
    "lotData": [
        {
            "lotNumber": 100001,
            "lotPrice": 0,
            "lotStatus": "READY",  
            "lotBidCount": 1
        },
        {
            "lotNumber": 100002,
            "lotPrice": 1000000,
            "lotStatus": "FINISH",  
            "lotBidCount": 10
        },
        {
            "lotNumber": 100003,
            "lotPrice": 0,
            "lotStatus": "CANCEL",  
            "lotBidCount": 0
        }
        {
            "lotNumber": 100004,
            "lotPrice": 30000,
            "lotStatus": "PROGRESS",  
            "lotBidCount": 5
        } 
    ]
}
```

* **`lotNumber`** : 경매번호
* **`lotPrice`** : 현재 가격 
* **`lotStatus`** : 경매 상태
  * READY : 경매 시작전
  * PROGRESS : 경매중
  * FINISH : 경매 종료
  * CANCEL : 출품 취소

* **`lotBidCount`** : 경매 응찰 건수 



> 유효하지 lotNumber가 포함된 경우, 유효한 lotNumber 에 한해서 응답이 내려가며, 유효하지 않은 lotNumber 는 생략이 됩니다.


