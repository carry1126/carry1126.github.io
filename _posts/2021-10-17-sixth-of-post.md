---
title: "jQuery"
date: 2021-10-17 20:30:00 -0400
categories: technique
---
서버개발에서 웹개발로 전환되었다. 나는 서버개발로 전향할라고 왔는데 압박하는 상황 속에서 개발을 하려고 하니 적응하기도 쉽지 않았다.   
웹개발은 익숙한 환경이다. 업무적으로는 마음에 들고 다만 script와 css를 잘 봐야된다는 것은 힘들다.   
퍼블리싱된 화면이 나왔는데 기능처리가 되게 하려고 하니 jQuery에 대한 정리가 필요할 꺼 같아서 간략히 정리해본다.   

[참조]<https://opentutorials.org/course/53>   

# jQuery란?     
자바스크립트의 생산성을 향상시켜주는 자바스크립트 라이브러리   
head나 body에 스크립트 관련 설정   
<script type="text/javascript" src="https://ajax.googleapis.com/ajax/libs/jquery/1.6.2/jquery.min.js"></script>   

# 이벤트 처리
이벤트를 처리하는 방법은 bind, unbind, trigger, live를 이용해서 다양한데 이벤트 헬퍼를 사용해서 처리할 수 있다.   
<script type="text/javascript">   
  function clickHandler(e) {   
       alert('thank you');   
  }   
  $(document).ready(function() {   
       $('#click_me').click(clickHandler);   
       $('#remove_event').click(function(e) {   
           $('#click_me').unbind('click', clickHandler);   
       });   
       $('#trigger_event').click(function(e) {   
           $('#click_me').trigger('click');   
       });   
  })   
</script>   

# ajax   
Asynchronous JavaScript and XML의 약자   
자바스크립트를 이용해서 비동기식으로 서버와 통신하는 방식, 이 때 XML을 이용한다.   
꼭 XML을 이용할 필요는 없고, 최근에는 json을 더 많이 이용한다.   
비동기식이란 여러가지 일이 동시적으로 발생한다는 뜻으로, 서버와 통신하는 동안 다른 작업을 할 수 있다는 의미   

$.ajax(settings)   
- jQuery를 이요한 ajax통신의 가장 기본적인 API   
- 주요속성
   data : 서버에 전송할 데이터, key/value 형식의 객체   
   dataType : 서버가 리턴하는 데이터 타입(xml, json, script, html)   
   type : 서버로 전송하는 데이터의 타입(POST, GET)   
   url : 데이터를 전송할 URL   
   success : ajax 통신에 성공했을 때 호출될 이벤트 핸들러   
   
   $.ajax({   
       url:'http://...',   
       dataType:'json',   
       type:'POST',   
       data:{'msg':$('#msg').val()},   
       success:function(result) {   
           if(result['result'] == true) {   
              $('#result').html(result['msg']);   
           }   
        }   
   });   
   
# 엘리먼트 제어
[참조]<https://opentutorials.org/course/53/51

# 페이징 처리
[참조]<https://mchch.tistory.com/140>   

totalData : 총 데이터 수   
dataPerPage : 한 페이지에 나타낼 데이터 수   
pageCount : 한 화면에 나타낼 페이지 수
currentPage : 현재 페이지   

function paing(totalData, dataPerPage, pageCount, currentPage) {   
  totalPage = Math.ceil(totalData / dataPerPage); //총 페이지 수   
  
  pageGroup = Math.ceil(currentPage / pageCount);   //페이지 그룹
  last = pageGroup * pageCount;   //화면에 보여질 마지막 페이지 번호  
  
  first = last - (pageCount - 1); //화면에 보여질 첫번째 페이지 번호   
  next = last + 1;   //다음 페이지
  prev = first - 1;  //이전 페이지
  ...
}   
