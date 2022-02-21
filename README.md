# seoulauction-api

## 경매 조회 API

### [GET] /api/lots

경매 번호에 매핑된 경매 작품번호의 정보를 조회합니다.

#### Request 
* **`saleNumber`** : 경매 번호 (필수값)
* **`lotNumbers`** : 경매 작품번호 (필수값)

##### Response
* **`saleNumber`** : 경매 번호
* **`lotNumber`** : 경매 작품번호
* **`lotPrice`** : 현재 가격
* **`lotTotalPrice`** : 수수료 포함 가격(+19.8%) 
* **`lotStatus`** : 랏 진행 상태 (FROM_DT , TO_DT)
  * READY : 경매 시작전
  * PROGRESS : 경매 중
  * FINISH : 경매 종료
  * CANCEL : 출품 취소
* **`lotBidCount`** : 경매 응찰 건수 
* **`lotEstimatePrice`**: 추정가 (by collectors 는 추정가 있음)
  * `from`
  * `to`


### 요청 예시

```sh
$ curl -XGET 'http://dev.seoulauction.xyz/api/lots?saleNumber=689&lotNumbers=1,2,3'
```


##### 상세 설명

* 경매 정보 조회 API 는 1초 간격으로 캐쉬 값이 갱신이 됩니다. 
* 즉, 1초 이내 동일정보 호출시 동일한 값이 확인 됩니다.



### 응답 예시

```json
{
	"lotData":[
		{
			"lotStatus":"PROGRESS",
			"lotTotalPrice":1437600,
			"lotPrice":1200000,
			"lotBidCount":8,
			"lotNumber":1,
			"estimatePrice":{
				"from":"800000",
				"to":"2000000"
			}
		},
		{
			"lotStatus":"PROGRESS",
			"lotTotalPrice":0,
			"lotPrice":0,
			"lotBidCount":0,
			"lotNumber":2,
			"estimatePrice":{
				"from":"800000",
				"to":"2000000"
			}
		},
		{
			"lotStatus":"PROGRESS",
			"lotTotalPrice":2396000,
			"lotPrice":2000000,
			"lotBidCount":1,
			"lotNumber":3,
			"estimatePrice":{
				"from":"2000000",
				"to":"4000000"
			}
		}
	],
	"saleNumber":689
}
```

> 유효하지 lotNumber가 포함된 경우, 유효한 lotNumber 에 한해서 응답이 내려가며, 유효하지 않은 lotNumber 는 생략이 됩니다.


