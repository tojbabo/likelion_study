# DAY 8.
---
1. 클래스 관계
   * has a 관계
    student.name: 학생 클래스가 이름(String 클래스)을 갖는다.

     * 클래스간의 lifecycle 관계
       자동차 <> 엔진(composition 관계): 엔진이 없으면 자동차 의미가 없다. 라이프사이클이 동일함
       *UML에서 꽉찬 마름모꼴*
       자동차 <> 라디오(aggregation 관계): 라디오 없어도 자동차 의미는 있음. 라이프사이클이 다름
       *UML에서 빈 마름모*
    


   * is a 관계(상속 관계)
    고양이 is a 애완동물
    *public class Dog **extends** Pet{ }*
    *UML에서 삼각형의 실선으로 표시, 부모 클래스에 대가리가 붙음*

---
#### 상속
* 생성자와 private은 상속이 안된다
* 
