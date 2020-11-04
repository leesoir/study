```java
public class Stack {
    
    List<String> colors = new ArrayList<>();
    
    public void stack() {
         System.out.println(this.colors);
    }
    
    public void push(String color) {
         this.colors.add(color);
    }
    
    public String pop() {
         String last = this.colors.get(this.colors.size()-1); // 마지막 인덱스 값
         this.colors.remove(this.colors.size()-1);
         return last;
    } // 가장 마지막에 위치한 color값을 리턴한다.
 
}


2) main() : push, pop을 통해 List에 값을 넣고 빼는 코드를 실행한다.
Stack s1 = new Stack();
// stack 객체 s1 생성

System.out.println("* push 시작 *");
s1.push("빨");
s1.push("주");
s1.push("노");
s1.push("초");
s1.push("파");
s1.push("남");
s1.push("보");
System.out.println("* push 종료 *");
// 현재 s1.colors = [빨, 주, 노, 초, 파, 남, 보]
s1.stack();

System.out.println("* pop 시작 *");
for(int i=0; i<7; i++)
s1.pop(); // push된 값들을 모두 제거
System.out.println("* pop 종료 *");
// 현재 s1.colors = [ ] (모두 pop해서 비었음)
}
```
