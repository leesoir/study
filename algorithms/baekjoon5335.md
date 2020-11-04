```java
package IOquiz;
import java.util.Scanner;
 
public class Ex04 {

    /*   문제) 화성 수학
    겨울 방학에 달에 다녀온 상근이는 여름 방학 때는 화성에 갔다 올 예정이다.
    화성에서는 지구와는 조금 다른 연산자 @, %, #을 사용한다.
    @는 3을 곱하고, %는 5를 더하며, #는 7을 빼는 연산자이다.
    따라서, 화성에서는 수학 식의 가장 앞에 수가 하나 있고, 그 다음에는 연산자가 있다.*/
 
    public static void main(String[] args) throws Exception{
         try{
             //           FileInputStream in = new FileInputStream("src/IOquiz/Ex04.txt");
             //           InputStreamReader rd = new InputStreamReader(in);
             //           BufferedReader breader = new BufferedReader(rd);
 
             Scanner sc = new Scanner(System.in);
             System.out.print("화성 수학식을 입력하세요 : ");
             String[] strs = sc.nextLine().split(" "); // 입력한 값을 문자열로 받아옴
             double num = Double.parseDouble(strs[0]); // strs의 첫 번째 글자는 무조건 숫자임. 
             // NumberFormatException 발생 문제 -> double타입을 Integer.parseInt로 해서. 실수형으로 받으려면 Double.parseDouble() 사용
​
             for(int k=1; k<strs.length; k++) {
                  if(strs[k].equals("@")) {
                      num *= 3;
                  } else if(strs[k].equals("%")) {
                      num += 5;
                  } else if(strs[k].equals("#")) {
                      num -= 7; 
                  }
             }
             System.out.println(Math.round(num*100)/100.0 + " ");
             // 문제점 : 10.4 # % @와 같이 숫자로 실수를 입력하면 NumberFormatException.
             // 구글링하면 다른 사람들은 printf 사용해서 푸는데 printf 사용하지 않고 소수점 둘째자리까지만 리턴하려면 어떻게 해야 할까? 
             // -> Math.round(값 * (자를 소수점자리*1)) / 자를 소수점자리.0
             // 이렇게 하면 자동으로 double타입으로 캐스팅된다!
             
         sc.close();
         
    } catch(Exception e) {
         e.printStackTrace();
    }
}
}
```
