# API


### __@ResponseBody 문자 반환__ : 리턴값이 ***문자***인 경우

+ [HelloController](https://github.com/journeytorainbow/spring_boot_study/blob/master/hello-spring/src/main/java/hello/hellospring/controller/HelloController.java) 클래스 `24~28라인` 설명
    + `@ResponseBody` : 이것을 사용하면 `viewResolver`를 사용하지 않는다. 대신 `HTTP`의 `응답 바디`에 리턴값으로 준 문자가 ***그대로*** 반환된다.
    + 실행 : http://localhost:8080/hello-string?name=spring
    + 결과값

```
hello! spring
```

### __@ResponseBody 객체 반환__ : 리턴값이 ***객체***인 경우

+ ★ ***API방식*** ★ : [HelloController](https://github.com/journeytorainbow/spring_boot_study/blob/master/hello-spring/src/main/java/hello/hellospring/controller/HelloController.java) 클래스 `30~47라인` 설명
    + `38~47라인` : 중첩 클래스(Hello) 선언
        + `getter/setter` 사용 : `자바빈(JavaBean) 규약`이라고 부른다. (프로퍼티 접근 방식이라고 부르기도 함.)
    + (★ ***핵심!!*** ★)`30~35라인` : 이와 같이 `@ResponseBody`를 사용하고, `객체`를 리턴하면 해당 `객체`가 `JSON`으로 변환됨.
    + 실행 : http://localhost:8080/hello-api?name=spring
    + 결과값

    ```
    {"name":"spring"}
    ```

    + 이와 같이 스프링은 `JSON`으로 반환하는 것이 디폴트로 셋팅이 되어있다. (원한다면 `XML`방식도 가능하지만, 트렌드상 `JSON`방식을 사용하는 것이 맞다!!)

    + `@ResponseBody` 동작 원리 (이미지 출처 : [강의 자료](https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-%EC%9E%85%EB%AC%B8-%EC%8A%A4%ED%94%84%EB%A7%81%EB%B6%80%ED%8A%B8/lecture/49605?tab=curriculum&speed=2))
        + 컨트롤러가 메소드 매핑이 되어있는지 확인하여 되어있다면, 해당 메소드를 호출한다. 이 때, `@ResponseBody` 어노테이션이 붙어있으면, `HTTP` `응답 바디`에 그대로 문자 내용을 직접 반환한다. 이 때, `viewResolver` 대신 `HttpMessageConverter`가 동작한다.
            + 기본 문자 처리(리턴값이 문자인 경우) : `StringHttpMessageConver`가 동작
            + 기본 객체 처리(리턴값이 객체인 경우) : `MappingJackson2HttpMessageConverter`가 동작
            + byte처리 등등 기타 여러가지 `HttpMessageConverter`가 기본으로 등록되어 있다.

    <img src="https://github.com/journeytorainbow/spring_boot_study/blob/master/%EC%8A%A4%ED%94%84%EB%A7%81_%EC%9B%B9%EA%B0%9C%EB%B0%9C_%EA%B8%B0%EC%B4%88/img/img_3.JPG?raw=true">


+ 참고 : 클라이언트의 `HTTP Accept헤더`(요청시 어떤 포맷으로 받고 싶은지 알려줌)와 서버의 컨트롤러 반환 타입 정보 두 가지를 조합하여 `HttpMessageConverter`가 선택된다. (자세한 것은 추후에 스프링 MVC 강의에서 다룬다고 한다.)