```java
package IOquiz;

 

//import java.io.BufferedReader;

//import java.io.FileInputStream;

//import java.io.InputStreamReader;

import java.util.Scanner;
public class Ex05 {

    /*문제) 핸드폰 요금
    동호는 새악대로 T 통신사의 새 핸드폰 옴머나를 샀다. 새악대로 T 통신사는 동호에게 다음 두 가지 요금제 중 하나를 선택하라고 했다.
 
    영식 요금제는 30초마다 10원씩 청구된다. 
    이 말은 만약 29초 또는 그 보다 적은 시간 통화를 했으면 10원이 청구된다. 만약 30초부터 59초 사이로 통화를 했으면 20원이 청구된다.
    민식 요금제는 60초마다 15원씩 청구된다. 
    만약 59초 또는 그 보다 적은 시간 통화를 했으면 15원이 청구된다. 만약 60초부터 119초 사이로 통화를 했으면 30원이 청구된다.
 
    동호가 저번 달에 새악대로 T 통신사를 이용할 때 통화 시간 목록이 주어지면 어느 요금제를 사용 하는 것이 저렴한지 출력하는 프로그램을 작성하시오.*/
 
    public static void main(String[] args) throws Exception{
//       FileInputStream in = new FileInputStream("src/IOquiz/Ex05_1");
//       InputStreamReader rd = new InputStreamReader(in);
//       BufferedReader breader = new BufferedReader(rd);
//
//       int count = Integer.parseInt(breader.readLine()); // 통화 개수
//       String[] strs = breader.readLine().split(" "); 
//       // 두 번째 줄의 문자열을 공백으로 나눠서 문자열 배열에 넣음
         
         Scanner sc = new Scanner(System.in);
         System.out.println("통화 개수를 입력하세요 : "); // 3
         int count = sc.nextInt();
         sc.nextLine();
         
         System.out.println("각 통화 시간을 입력하세요 : "); // 40 40 40
         String[] strs = sc.nextLine().split(" "); // 입력받은 수를 공백으로 나눔
         int[] ints = new int[strs.length];
         
         for(int i=0; i<strs.length; i++) {
             ints[i] = Integer.parseInt(strs[i]);
         } // 입력받은 값들을 숫자 배열에 캐스팅하여 넣어줌
         
         int youngsikBill = 0; // 영식 요금제로 구한 요금
         int minsikBill = 0; // 민식 요금제로 구한 요금
 
         for(int k=0; k<count; k++) {
             int totalTime = ints[k];
             
             youngsikBill += ((totalTime / 30) + 1)*10; // 영식 요금제 : 30초마다 10원
             minsikBill += ((totalTime / 60) + 1)*15; // 민식 요금제 : 60초마다 15원
             // count 수만큼 돌면서 전체 요금을 계산하므로 요금제 +=을 해줘야 함(그렇지 않으면 k가 증가할때마다 요금값 리셋)
             
             // check : 두 요금제의 계산 원리 생각해보기
         } 
         
         
         if(youngsikBill < minsikBill) {
             System.out.println("Y " + youngsikBill); 
         } else if(minsikBill < youngsikBill) {
             System.out.println("M " + minsikBill);
         } else if(minsikBill == youngsikBill) {
             System.out.println("Y M " + youngsikBill);
         }
         
         // 문제 : 3 \n 61 61 61을 입력하면 영식, 민식 요금제 모두 90이 나와야 하는데 M 60으로 나옴
         // 해결 -> 요금제 += 해야함.
         
         sc.close();

    }

}
```
