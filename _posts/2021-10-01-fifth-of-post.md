---
title: "통신관련 정의, ModelMapper"
date: 2021-10-01 21:00:00 -0400
categories: technique
---
ISP(일반결제) 관련 카드업무를 하면서 관련 기술을 접하게 되었는데 사용하는 법을 잘 모르니 이해가 안 됐다.   
팀장님이 열심히 설명은 해주는데 소화하는 입장에서는 정리가 안되서 답답했다.   
구글링 해서 찾아보니 관련 내용이 나와 조금은 정리가 되는 느낌이었다.   

API GateWay : API 서버 앞단에서 모든 API 서버들의 엔드포인트를 단일화 해주는 또다른 서버   
API에 대한 인증과 인가 기능을 가지고 있으며, 메세지의 내용에 따라 어플리케이션 내부에 있는 마이크로서비스로 라우팅하는 역할을 담당   
[참조]<https://velog.io/@tedigom/MSA-%EC%A0%9C%EB%8C%80%EB%A1%9C-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-3API-Gateway-nvk2kf0zbj>

TCP(Transmission Control Protocol) : IP 네트워크의 두 컴퓨터 간의 연결 지향 통신을 위한 전송 계층 호스트 간 프로토콜   
TCP는 가상 포트를 사용하여 두 컴퓨터 간의 물리적 연결을 재사용 할 수 있는 가상 종단 간 연결을 만듦

HTTP API(REST API 포함)   
[참조]<https://www.inflearn.com/questions/126743>

# ModelMapper   
Property Mapping   
source의 get메서드와 destination의 set메서드로 구헝   
typeMap.addMapping(Source::getFirstName, Destination::setName);   
map().setXXX(source.getXXX)

Converters   
destination 타입을 전환할 때 위임한다.   

Converters 작성 2가지 방법   
1.AbstractConverter로 확장   

Converter<String, String> toUpperCase = new AbstractConverter<String, String>() {   
  protected String convert(String source) {   
    return source == null ? null : source.toUpperCase();    
  }   
};   

2.Converter 인터페이스(현재 매핑 request와 관련된 정보를 포함한 MappingContext를 내포) 구현   

Converter<String, String> toUpperCase = new Converter<String, String>() {   
 public String convert(MappingContext<String, String> context) {   
  return context.getSource() == null ? null : context.getSource().toUpperCase();   
 }   
};     

3.기타 using converters with properties    

Converter<String, String> toUppercase =   
    ctx -> ctx.getSource() == null ? null : ctx.getSource().toUppercase();   
    
typeMap.addMappings(mapper -> mapper.using(toUppercase).map(Person::getName, PersonDTO::setName));   

lamda 표현식 사용   
=> typeMap.addMappings(mapper -> mapper.using(ctx -> ((String) ctx.getSource()).toUpperCase())   
         .map(Person::getName, PersonDTO::setName));   
         
[참조]<http://modelmapper.org/user-manual/converters/>   
[참조]<https://amydegregorio.com/2018/01/17/using-custom-modelmapper-converters-and-mappings/>   
[참조]<http://modelmapper.org/user-manual/property-mapping/#converters>
