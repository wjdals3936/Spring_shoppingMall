# 🛒 Spring_shoppingMall
자바 코드로 구현한 쇼핑몰, Spring MVC 구조로 고도화 프로젝트   
 <br>
 ## 👨‍💻 프로젝트 소개
 온라인 신발 판매 쇼핑몰 사이트 'NonAge'입니다.  
 ![image](https://github.com/wjdals3936/Spring_shoppingMall/assets/101387993/e9c26701-433f-4ea1-a937-24eaf16ef2b2)

 
 ## 📅 프로젝트 기간
	* 23.08.28 ~ 23.08.30   
  
###  멤버 구성 및 개발 파트
👩&nbsp; <a href="https://github.com/wjdals3936">박정민</a> - Member(로그인) <br>
👨‍🦰 &nbsp; <a href="https://github.com/Lee-HyunSoo">이현수</a> - Admin(관리자) <br>
👩 &nbsp;<a href="https://github.com/dahyunhan">한다현</a> - QnA(고객문의) <br>
👨‍🦰 &nbsp; 한신우 - Order(주문하기) , Cart(장바구니) <br>
 <br>
 ### 🌐 개발 환경  
 **JAVA** : jre1.8.0_251      
 **IDE** : sts-3.8.4.RELEASE   
 **FrameWork** : Spring 4.1.1   
 **Database** : Oracle DB   
 **Tool** : SqlDeveloper   
 **ORM** : Mybatis   
 <br> 
 
  ### 🚦 사전 협의된 개발 규칙 
    파라미터명은 카멜케이스로  
    Controller, Service, DAO 메서드 URI 명과 동일하게  
    Controller를 통해 들어오는 파라미터는 로그로 확인  
    RequestMethod는 기존 jsp 요청을 최대한 변경하지 않는 선에서  
    GET, POST 분리 사용  
    Controller에 어떤 역할을 하는지 간단히 주석  
  <br>
	<br>
 
   ### 📁 패키지 구조
![image](https://github.com/wjdals3936/Spring_shoppingMall/assets/101387993/dbb41efd-0763-46ec-8837-dcf82ef8ade9)

  ### 🗃️ 기존 코드 분석
    기존 servlet : 사용한 코드 spring 스타일로 변경  
    기존 DAO : JDBC template를 사용한 부분을 mybatis로 변경
  <br> 
  
  ### ✅ 컨트롤러에 있는 비즈니스 로직을 서비스로 옮김
```
/**
	 * selectSeqOrderIng메서드로 받아온 값을 이용해
	VO객체에 이름과 총가격을 더해 List에 담고 리턴해줌
	 * @param id 사용자 ID 값
	 * @return List<OrderVO> VO객체 리스트 반환
	 */
	@Transactional(readOnly = true)
	public List<OrderVO> returnVO(String id) {
		List<Integer> oseqList = selectSeqOrderIng("one");
		List<OrderVO> orderList = new ArrayList<OrderVO>();
		for (int oseq : oseqList) {
			List<OrderVO> orderListIng = listOrderById("one", "1", oseq);
			OrderVO orderVO = orderListIng.get(0);
			orderVO.setPname(orderVO.getPname() + " 외 " + (orderListIng.size() - 1) + "건");
			int totalPrice = calTotalPrice(orderListIng);
			orderVO.setPrice2(totalPrice);
			orderList.add(orderVO);
		}
		return orderList;
	}
```
### ☑️ 원래 dao에서 한번에 쿼리문 실행하던 걸 나눔
```
/**
	 * 받아온 장바구니 목록을 id를 기준으로 db에 저장
	 * 1. 주문 테이블에 새로운 주문을 추가한다.
	 * 2. 장바구니 목록에 해당하는 상품 번호와 양을 주문 상세 테이블에 추가한다.
	 * @param cartList 	추가할 장바구니 목록
	 * @param id		주문한 유저의 아이디
	 * @return maxOSEQ  추가한 주문 시퀀스 반환
	 *
	 */
	public int insertOrder(List<CartVO> cartList, String id) {
		int maxOSEQ = dao.selectMaxOseq();
		dao.insertOrder(id);
		for (CartVO cart : cartList) {
			dao.insertOrderDetail(cart, maxOSEQ);
			dao.updateCartResult(cart.getCseq());
		}
		return maxOSEQ;
	}
```

 ### 💬 컨트롤러 주석 정리한 사진
 ![image](https://github.com/wjdals3936/Spring_shoppingMall/assets/101387993/cdf5fb23-d41f-48b2-aaac-081483c15f28)
    
    
 ### 🖥️ 로그 찍은 콘솔 사진
 ![image](https://github.com/wjdals3936/Spring_shoppingMall/assets/101387993/9bbc9743-5ace-4bee-9b5c-c19c731a24b4)
     
 ### 🤔 개선할 점
 개인적인 개선점이지만 VO > Mybatis model/mapper xml > DAO > Service > Controller 순으로 파일별로 코드 구현을 하다 보니 로직도 헷갈리고
 ```
Mybatis Mapper XML 오류 :: There is no getter for property named '*' in '*'
```
와 같은 에러도 많이 나고 수정할 부분도 오히려 많아져서 다음부터는 단위 기능별로 구현해야 함을 뼈져리게 느꼈다.
		
