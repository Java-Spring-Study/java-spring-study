## HTTP Methods

### The GET Method

- 웹 서비스 개발에 주로 사용하는 메서드
- be used to request data from a specified resource
- **요청**
    
    클라이언트가 서버에게 웹페이지를 보여달라고 말하는 것
    
- **응답**
    
    서버가 클라이언트에게 요청받은 것에 대한 대답으로 웹페이지 내용을 표현하기 위해 HTML 문서롤 주는 것
    
- **Some notes on GET requests**
    - GET requests can be cached
    - GET requests remain in the browser history
    - GET requests can be bookmarked
    - GET requests should never be used when dealing with sensitive data
    - GET requests have length restrictions
    - GET requests are only used to request data (not modify)

<aside>
🔗 www.example.com?id=mommoo&pass=1234

</aside>

- 클라이언트의 데이터를 URL 뒤에 붙여서 보낸다
- URL 뒤에 “?” 마크를 통해 URL의 끝을 알리는 동시에 데이터 표현의 시작점을 알린다.
- 데이터는 key와 value 쌍으로 넣어야 한다. 위의 예시 링크에서 key는 id와 pass이고, value는 mommoo와 1234이다.
- 중간에 “&” 마크는 구분자이다. 2개 이상의 key - value 쌍 데이터를 보낼 때는 “&” 마크로 구분해준다.
- URL에 붙이므로 HTTP Packet의 헤더에 포함되어 서버에 요청한다.

---

> GET 방식에서 바디에 넣을 특별한 내용이 없으므로 바디가 빈 상태로 전송된다.
> 
> 
> 헤더의 내용 중 바디의 데이터를 설명하는 Content-Type이라는 헤더필드는 들어가지 않는다.
> 
> URL 형태로 표현되므로 특정 페이지를 다른사람에게 접속하게 할 수 있다.
> 
> 간단한 데이터를 넣도록 설계되었기 때문에 데이터를 보내는 양의 한계가 있다.
> 

### The POST Method

- be used to send data to a server to create/update a resource
- **Some notes on POST requests**
    - POST requests are never cached
    - POST requests do no remain in the browser history
    - POST requests cannot be bookmarked
    - POST requests have no restrictions on data length

> GET 방식과는 달리 데이터 전송을 기반으로 한 요청 메서드
> 
> 
> **데이터를 URL에 붙여서 보내지 않고 바디에 넣어서 보낸다.**
> 
> 헤더필드 중 바디의 데이터를 설명하는 Content-Type이라는 헤더필드가 들어가고, 어떤 데이터 타입인지 명시한다.
> 
> 1. **application/x-www-form-urlencoded**
>     
>     GET 방식과 마찬가지로 바디에 key와 value 쌍으로 데이터를 넣는다.
>     
>     동일하게 구분자는 “&”를 쓴다.
>     
> 2. **text/plain**
>     
>     바디에 단순 텍스트를 넣는다.
>     
> 3. **multipart/form-data**
>     
>     파일 전송할 때 많이 쓴다.
>     
>     바디의 데이터를 바이너리 데이터롤 넣는다는 것을 알려준다.
>     
> 
> 컨텐츠 타입을 꼭 명시해줘야 하는데, 명시하지 않은 경우 보통 첫 번째 컨텐츠 타입으로 설정된다.
> 

### Compare GET vs. POST

|  | GET | POST |
| --- | --- | --- |
| BACK button/Reload | Harmless | Data will be re-submitted (the browser should alert the user that the data are about to be re-submitted) |
| Bookmarked | Can be bookmarked | Cannot be bookmarked |
| Cached | Can be cached | Not cached |
| Encoding type | application/x-www-form-urlencoded | application/x-www-form-urlencoded or multipart/form-data. Use multipart encoding for binary data |
| History | Parameters remain in browser history | Parameters are not saved in browser history |
| Restrictions on data length | Yes, when sending data, the GET method adds the data to the URL; and the length of a URL is limited (maximum URL length is 2048 characters) | No restrictions |
| Restrictions on data type | Only ASCII characters allowed | No restrictions. Binary data is also allowed |
| Security | GET is less secure compared to POST because data sent is part of the URLNever use GET when sending passwords or other sensitive information! | POST is a little safer than GET because the parameters are not stored in browser history or in web server logs |
| Visibility | Data is visible to everyone in the URL | Data is not displayed in the URL |
1. **POST 방식이 GET 방식보다 보안 측면에서 더 좋다?**
    
    POST든 GET이든 보내는 데이터는 전부 클라이언트 측에서 볼 수 있다.
    
    GET 방식은 URL에 데이터가 표시되어 별다른 노력 없이 볼 수 있지만, 두 방식 전부 보안을 생각한다면 암호화 해야 한다.
    
2. **GET 방식이 POST 방식보다 속도가 빠르다?**
    
    빠른 것이 맞다.
    
    GET 방식의 요청은 캐싱 때문에 빠른 것이다.
    
    - Caching
        
        한 번 접근 후, 또 요청할 시 빠르게 접근하기 위해 데이터를 저장한다.
