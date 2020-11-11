# MVC와 템플릿 엔진

+ `MVC`
    + M : Model
    + V : View
        + 화면을 그리는 것에 관련된 일만 담당
    + C : Controller
        + 비즈니스 로직 및 뒷단에 관련된 일만 담당

---

### __Controller__

+ [HelloController](https://github.com/journeytorainbow/spring_boot_study/blob/master/hello-spring/src/main/java/hello/hellospring/controller/HelloController.java) 클래스 `17~21라인` 설명
    + `@RequestParame`의 `required`라는 옵션의 기본값은 `true`이다. 따라서, `name`파라미터에 값을 주지 않을 경우 예외가 발생하게 된다.
        + [참고 링크](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/web/bind/annotation/RequestParam.html#required--)

### __View__

+ [resources/template/hello-template.html](https://github.com/journeytorainbow/spring_boot_study/blob/master/hello-spring/src/main/resources/templates/hello-template.html)


### __실행__

+ http://localhost:8080/hello-mvc?name=spring

+ 동작 원리 설명 (출처 : [강의 자료](https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-%EC%9E%85%EB%AC%B8-%EC%8A%A4%ED%94%84%EB%A7%81%EB%B6%80%ED%8A%B8/lecture/49605?tab=curriculum&speed=2))
    + 웹브라우저에서 localhost:8080/hello-mvc를 넘기면, 내장 톰캣 서버가 이것을 스프링에 넘긴다. 스프링은 컨트롤러에 메서드 매핑이 되어있는지 확인하여, 돼있다면, 해당 메서드를 호출하고 해당 메서드가 문자를 리턴(hello-template)하면 `viewResolver`(view를 찾아주고, 템플릿 엔진을 연결해주는 역할)가 해당 화면을 찾아 처리한다.
        + 이 때, `model`에 키값으로는 `name`을 값으로는 `spring`을 넘겨줌.
        + `Thymeleaf` 템플릿 엔진이 렌더링하여 변환된 html을 클라이언트 쪽으로 반환한다.

<img src="https://github.com/journeytorainbow/spring_boot_study/blob/master/%EC%8A%A4%ED%94%84%EB%A7%81_%EC%9B%B9%EA%B0%9C%EB%B0%9C_%EA%B8%B0%EC%B4%88/img/img_2.JPG?raw=true">