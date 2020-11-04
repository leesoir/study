```java
/* 문제) 책이름으로 작가명 찾기
> 책이름을 입력 받으면 책의 작가명을 출력하는 프로그램 
​
＊ 장르별로 책과 작가의 쌍이 n개 들어있다.
＊ 사용자로부터 책이름을 입력 받는다. 
＊ 책이름에 해당하는 작가명을 출력한다.
예) 어린왕자의 작가명은 생텍쥐페리 입니다. */
​
​
​
public class searchTest {
    public static void main(String[] args) {
         // {장르1={책제목1=작가1, 책제목2=작가2}, 장르2={책제목1=작가1, 책제목2=작가2}}
         // {
         //     자기계발={더 해빙=이서윤,홍주연, 말 그릇=김윤나, 메모의 마법=마에다 유지},
         //     소설={어린왕자=생텍쥐페리, 아몬드=손원평, 나미야 잡화점의 기적=히가시노 게이고, 해변의 카프카=무라카미 하루키},
         //     과학={시간은 흐르지 않는다=카를로 로벨리, 코스모스=칼 세이건, 평행우주=미치오 카쿠}
         // }
 
         Map<String, Map<String, String>> bookMap = new HashMap<>();
 
         Map<String, String> map1 = new HashMap<>();
         map1.put("더 해빙", "이서윤,홍주연");
         map1.put("말 그릇", "김윤나");
         map1.put("메모의 마법", "마에다 유지");
 
         Map<String, String> map2 = new HashMap<>();
         map2.put("어린왕자", "생텍쥐페리");
         map2.put("아몬드", "손원평");
         map2.put("나미야 잡화점의 기적", "히가시노 게이고");
         map2.put("해변의 카프카", "무라카미 하루키");
 
         Map<String, String> map3 = new HashMap<>();
         map3.put("시간은 흐르지 않는다", "카를로 로벨리");
         map3.put("코스모스", "칼 세이건");
         map3.put("평행우주", "미치오 카쿠");
 
         bookMap.put("자기계발", map1);
         bookMap.put("소설", map2);
         bookMap.put("과학", map3);
         System.out.println(bookMap);
 
         // 책 이름 입력
         Scanner sc = new Scanner(System.in);
         System.out.print("책이름을 입력해주세요: ");
         String searchBook = sc.nextLine();
 
         // TODO: 구현하기
         Set<String> bookMapKey = bookMap.keySet(); // 자기계발, 소설, 과학
         Iterator<String> iter = bookMapKey.iterator(); 
         // bookMap의 키 값들을 모은 Set 객체를 읽어오는 Iterator 객체 iter
 
         boolean status = false;
         while(iter.hasNext()) { // iter는 while문을 돌면서 bookMap의 키값을 읽어온다.
             String key = iter.next(); // 처음 실행 시 : iter는 첫 번째 key값인 "자기계발"을 가리킨다.
             if(bookMap.get(key).containsKey(searchBook)) {
                  // bookMap.get(key)는 "자기계발"을 key값으로 하는 Map 객체(즉 bookMap의 value값)를 의미하고, contains(searchBook)은 그 Map 객체들 중 searchBook을 key값으로 가진 객체의 존재 여부를 리턴한다.
                  System.out.println(searchBook + "의 저자는 " + bookMap.get(key).get(searchBook) + "입니다."); // searchBook을 key값으로 가진 객체가 있을 경우 현재 key값의 value(=Map<String, String>)들 중 searchBook을 key값으로 가진 객체를 불러온다.
                  status = true; // status는 제어변수이다. 
             }
         }
         
         if(status == false) {
             System.out.println("찾는 책이 존재하지 않습니다.");
         }
 
 
         sc.close();
 
    }
}
```
