# seoulauction-api
seoulauction-api

# Rest API

인증 완료 후, 다음의 페이지로 리다이렉트

```
https://seoulauction.com/ssg/page...
```

---

## 경매상태

경매 상태 확인 API

```
[Request]
POST /ssg/lots/status/{saleNo}/{lotNo}
Host: https://seoulauction.com

# Headers
Content-Type: application/x-www-form-urlencoded

# Body
HTTP/1.1 200 OK		
Content-type: application/json;charset=UTF-8		
{		
  "message": "success",		
  "data": {		
    status : "ongoing"		
  }		
}
```

```
**[Response]**

# 200
{
  "result": "success",
  "data": {
		"status": "ongoing" # status: enum(ongoing/end/success/bought) - (진행중/낙찰/유찰)
  }
}

# 400
{
  "result": "error",
  "message": "invalid params"
}
```

---

## 가격조회

해당 랏의 가격 정보

```
**[Request]**
POST /ssg/lots/price
Host: https://seoulauction.com/api/v1

# Headers
Content-Type: application/x-www-form-urlencoded
X-Custom-Provider-Secret: sa-ssg-secret-key

# Body
{
  "sale": "123",
  "lot": "1234"
}
```

```
**[Response]**

# 200
{
  "result": "success",
  "data": {
		"price": "12000000" # number
  }
}

# 400
{
  "result": "error",
  "message": "invalid params"
}
```

---

## 응찰하기

응찰하기 버튼 클릭 후, 인증 요청.

```
Webview.open("https://seoulauction.com/ssg/autorize?uid=sa-ssg-11119999")

Webview.open("https://seoulauction.com/ssg/autorize?cid=11119999")

--- 구현 ---
/views/ssg/authorize.jsp

--> 버튼 클릭시, 네이티브의 window.webkit.closeWebview();
```

![deb78b4775eaac7999949c4a7c47d333635f7794.png](Rest%20API%2078f62835e8a84623a31b9f8c150969e6/deb78b4775eaac7999949c4a7c47d333635f7794.png)

```
**[Request]**
POST /ssg/authorize
Host: https://seoulauction.com/api/v1

# Headers
Content-Type: application/x-www-form-urlencoded
X-Custom-Provider-Secret: sa-ssg-secret-key

# Body
{
  "uid": "sa-ssg-11119999"
}
```

```
**[Response]**

# 200
{
  "result": "success"
}

# 400
{
  "result": "error",
  "message": "invalid uid"
}
```
