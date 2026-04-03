# DAY 5.
---
#### 배열

*자바에서 데이터를 저장하는 방법 3가지*
1. 변수
   - 필요한 데이터 갯수만큼 선언해줘야 함(관리가 어려움)

2. 배열
   - 여러개의 데이터 저장
   - 데이터 갯수와 상관없이 하나의 변수만 활용
   - 동이한 자료형만 저장(Java에선)
   - 크기 변경이 불가
   - 배열 자체는 참조형, 안에 저장되는 데이터는 기본형 참조형 모두 가능
  
3. 컬렉션
   - 배열과 같은 특성
   - 자료형이 달라도 저장 가능
   - 자동으로 크기 변환도 가능
   - 컬렉션 자체는 참조형, 데이터도 참조형만 가능(기본형은 Wrapper 클래스를 이용해 저장가능)
   - 종류 3가지
        * List 객체
          저장 순서가 있음. 중복 가능

        * Set 객체
          저장 순서가 없음. 중복 불가

        * Map 객체
          이름하고 값을 쌍으로 저장(key-value 쌍으로 저장)
          hash-table을 통한 탐색이 List/Set보다 우월하게 빠르다
  
**Wrapper 클래스**
    *기본형 데이터 8개에 해당되는 클래스를 의미*

    byte        | Byte
    short       | Short
    int         | Integer
    long        | Long
                |
    float       | Float
    double      | Double
                |
    char        | Character
                |
    boolean     | Boolean

---
#### 배열
문법: (자료형)[] (변수명) = new (자료형)[(크기)]
*new 키워드를 이용했기 때문에 heap 메모리에 생성, 배열 안은 자동으로 초기화됨*
각 요소는 인덱스로 접근하며, 0부터 시작

비정방형 배열: 각 행마다 열의 갯수가 다른 배열

* 배열에 없는 요소(배열 길이 밖) 접근시 (*ArrayIndexOutofBoundsException*) 에러 발생.
  <pre>
  {
    String[] names = {"a","b"}; 
    int[] num = new int[] {1,2,3,4}
    // 이런 방식으로 하면 크기설정이 따로 필요없다.
    
    int[][] ber = new int[2][];
    ber[0] = new int[2];
    ber[1] = new int[2];
    // 2차원 배열의 경우 이렇게 하자
    
    
    for(String n: names){
        // 이런방식으로도 사용이 가능하다
    }

  }
  </pre>
  
---
Command Line Arguments
main method에 파라미터로 있는 String[] args란?
프로그램 시작시에 값을 입력해 줄 수 있다.
*숫자로 넣어도 String으로 입력이 되기 때문에 유의*