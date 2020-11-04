```java
package IOquiz;

/*

 * 문제) 주사위 세개 1에서부터 6까지의 눈을 가진 3개의 주사위를 던져서 다음과 같은 규칙에 따라 상금을 받는 게임이 있다.
 * 같은 눈이 3개가 나오면 10,000원+(같은 눈)*1,000원의 상금을 받게 된다. 같은 눈이 2개만 나오는 경우에는 1,000원+(같은 눈)*100원의 상금을 받게 된다. 모두 다른 눈이 나오는 경우에는 (그 중 가장 큰 눈)*100원의 상금을 받게 된다.
 * 예를 들어, 3개의 눈 3, 3, 6이 주어지면 상금은 1,000+3100으로 계산되어 1,300원을 받게 된다. 또 3개의 눈이 2, 2, 2로 주어지면 10,000+21,000 으로 계산되어 12,000원을 받게 된다. 3개의 눈이 6, 2, 5로 주어지면 그중 가장 큰 값이 6이므로 6*100으로 계산되어 600원을 상금으로 받게 된다.
 * 3개 주사위의 나온 눈이 주어질 때, 상금을 계산하는 프로그램을 작성 하시오.

 */

import java.util.Scanner;
public class Ex06_re {
    public static void main(String[] args) {
         Scanner sc = new Scanner(System.in);
     
         System.out.print("주사위 번호를 입력하세요 : ");
         String diceStr = sc.nextLine();
         String[] diceStrs = diceStr.split(" ");
         int prize = 0;
         int max = 0;
         int[] dices = new int[diceStrs.length];
         int[] checkArr = new int[7]; // 0~6까지의 인덱스값을 가지는 checkArr. 해당 배열로 나온 주사위 수의 개수를 확인한다.
         
         for(int i=0; i<diceStrs.length; i++) {
             dices[i] = Integer.parseInt(diceStrs[i]);
         } // 문자열로 된 주사위 값을 숫자로 바꿔 숫자 배열 dices에 넣음
    
         for(int i=0; i<dices.length; i++) {
             checkArr[dices[i]] += 1; 
             // 해당 값의 checkArr값을 1씩 증가시킴. 주사위 값이 3 3 이면 checkArr[3]은 2가 됨.
         }

         for(int i=1; i<checkArr.length; i++) {
             if(checkArr[i] == 0) {
                  continue; 
                 // 해당 인덱스값은 주사위 값이 아니므로 아래 문장을 실행하지 않고 바로 i를 증가
             } else if(checkArr[i] == 3) {
                  // 같은 수가 3개 나온 경우
                  prize = 10000 + (i * 1000);
                  break; // break문을 지정해 줘야 마지막의 else if문을 돌지 않는다.
             } else if(checkArr[i] == 2) {
                  // 같은 수가 2개 나온 경우
                  prize = 1000 + (i * 100);
                  break;
             } else if(checkArr[i] == 1){
//                if(checkArr[i] > max) {
//                    max = checkArr[i]; // 현재 값이 max값보다 크면 해당 값을 최대값으로 지정
//                } // 해당 if문을 제거해도 됨 : 1인 인덱스만 도므로, 자동으로 값으로 1을 가지는 최대 인덱스값이 구해지게 된다.

                  max = checkArr[i];
                  prize = max * 100;

             }
         }
         
         System.out.println("상금은 " + prize + "원입니다.");

         // 문제점 : 3 3 6 입력 시 상금은 100원이 된다. 
         // 해결 -> 같은 주사위 값이 3개, 2개 나온 경우 break문을 추가해야 한다. break문을 추가하지 않으면 마지막 else-if 문에 들어가
         // prize가 최종적으로 다시 구해지게 된다.
        
         sc.close();
        
    } 

}
```
