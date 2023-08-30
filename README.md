# 🛒 Spring_shoppingMall
자바 코드로 구현한 쇼핑몰, Spring MVC 구조로 고도화 프로젝트   

 ## 👨‍💻 프로젝트 소개
 온라인 신발 판매 쇼핑몰 사이트 'NonAge'입니다.   

 ## 📅 프로젝트 기간
	* 23.08.28 ~ 23.08.30   
 
 ###  멤버 구성 및 개발 파트
<a href="https://github.com/wjdals3936">박정민</a> - Member(로그인) <br>
<a href="https://github.com/Lee-HyunSoo">이현수</a> - Admin(관리자) <br>
<a href="https://github.com/dahyunhan">한다현</a> - QnA(고객문의) <br>
한신우 - Order(주문하기) , Cart(장바구니) <br>

 ### 🌐 개발 환경  
 **JAVA** : jre1.8.0_251      
 **IDE** : sts-3.8.4.RELEASE   
 **FrameWork** : Spring 4.1.1   
 **Database** : Oracle DB   
 **Tool** : SqlDeveloper   
 **ORM** : Mybatis   
 

  ### 🗃️ 기존 코드 분석
    기존 servlet : 사용한 코드 spring 스타일로 변경  
    기존 DAO : JDBC template를 사용한 부분을 mybatis로 변경
  <br>  
	<br>
 
  ### 🚦 사전 협의된 개발 규칙 
    파라미터명은 카멜케이스로  <br>
    Controller, Service, DAO 메서드 URI 명과 동일하게  <br>
    Controller를 통해 들어오는 파라미터는 로그로 확인  <br>
    RequestMethod는 기존 jsp 요청을 최대한 변경하지 않는 선에서  <br>
    GET, POST 분리 사용  <br>
    Controller에 어떤 역할을 하는지 간단히 주석  <br>
  <br>
	<br>
 
   ### 📁 패키지 구조
		
 
  ### 💬 컨트롤러 주석 정리한 사진
		기존 컨트롤러에 있는 비즈니스 로직들을 서비스로 이동
 
  ### 로그 찍은 콘솔 사진
	 
		
