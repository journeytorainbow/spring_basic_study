# View 환경설정


> ## Welcome Page 만들기

+ **방법1** : 스프링 부트가 제공하는 Welcome Page 기능 
    + [static/index.html](https://github.com/journeytorainbow/spring_boot_study/blob/master/hello-spring/hello-spring/src/main/resources/static/index.html)을 올려두면 Welcome Page기능을 제공
        + 참고 링크 : [스프링 부트 매뉴얼](https://docs.spring.io/spring-boot/docs/current/reference/html/spring-boot-features.html#boot-features-webflux-welcome-page)

+ **방법2** : `Thymeleaf` 템플릿 엔진
    + 참고 링크
        + [Thymeleaf 공식 사이트](https://www.thymeleaf.org/)
        + [스프링 공식 튜토리얼](https://spring.io/guides/gs/serving-web-content/)
        + [스프링 부트 매뉴얼](https://docs.spring.io/spring-boot/docs/2.3.1.RELEASE/reference/html/spring-boot-features.html#boot-features-spring-mvc-template-engines)
    + [HelloController 클래스](https://github.com/journeytorainbow/spring_boot_study/blob/master/hello-spring/hello-spring/src/main/java/hello/hellospring/controller/HelloController.java) 코드 설명
        + `@GetMapping("hello")`
            + `Get`은 HTTP요청 메서드 `GET` 메서드를 의미 
            + `"hello"` : 해당 url과 매칭됨
        + `return "hello";` : `resources/templates`에서 문자열(`hello`)와 일치하는 `.html`을 찾아서 렌더링하라는 의미
            + 참고 : `IntelliJ`는 `"hello";`를 `Ctrl+마우스 좌클릭`하면 해당 `.html`로 이동하는 기능을 제공 
    + [resources/templates/hello.html](https://github.com/journeytorainbow/spring_boot_study/blob/master/hello-spring/hello-spring/src/main/resources/templates/hello.html) 코드 설명
        + `data`는 `HelloController`에서 `attributeName`(key)이고, 실제 화면에 보여지는 것은 `attributeValue`로 준 값이다.
    + `Thymeleaf` 템플릿 엔진 동작 확인하기
        + 실행 후, http://localhost:8080/hello 로 접속
    + 동작 환경 그림(출처 : [강의 자료](https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-%EC%9E%85%EB%AC%B8-%EC%8A%A4%ED%94%84%EB%A7%81%EB%B6%80%ED%8A%B8/lecture/49605?tab=curriculum&speed=2))
        + 컨트롤러에서 리턴값으로 문자를 반환하면 뷰 리졸버(`viewResolver`)가 해당 화면을 찾아서 처리한다.
            + 스프링 부트 템플릿 엔진 기본 `viewName`매핑
                + `resources:templates/ + {viewName(리턴값으로 준 문자)} + .html`

    <img src="https://github.com/journeytorainbow/spring_boot_study/blob/master/%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8_%ED%99%98%EA%B2%BD%EC%84%A4%EC%A0%95/img/img_10.JPG?raw=true">

+ 참고
    + `spring-boot-devtools`라이브러리를 추가하면, `html`파일을 컴파일만 해주면 서버 재시작 없이 `View`파일 변경이 가능하다.
        + [설정 방법 링크](https://lejewk.github.io/springboot-devtool/)
        + IntelliJ 컴파일 방법 : `build - Recompile`