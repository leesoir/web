```java
package com.javalec.quiz;
import java.util.Scanner;

public class Quiz03 {
	public static void main(String[] args) {
		
 		//      1. Scanner를 사용하여 6개의 데이터를 입력 받고, 이들을 nums 배열에 저장

		//		2. 입력 받은 값 중, 20 이상 100 이하인 원소만 출력

		//		3. 입력 받은 값 중, 최댓값과 최솟값을 출력
		//		int max = nums[0];
		//		int min = nums[0];
		//		(for문 사용)
		//		System.out.println("최댓값 : " + max);
		//		System.out.println("최댓값 : " + min);

		//		4. 오름차순(작은->큰)으로 정렬하여 모든 원소를 출력  ==> 버블 정렬 알고리즘 검색해서 ... 

		Scanner sc = new Scanner(System.in);
		int nums[] = new int[6];
		
		// 1) 6개의 데이터를 입력받고 이를 nums에 저장
		for(int i=0; i<nums.length; i++) {
			System.out.println(i + "번째 원소 >");
			nums[i] = sc.nextInt();
		} 

		System.out.println("입력 완료!");

		// 2) 20~100 사이 원소만 출력하기
		System.out.print("20 이상 100 이하 원소 > [ ");
		for(int i=0; i<nums.length; i++) {
			if(nums[i] >= 20 && nums[i]<=100) {
				System.out.print(nums[i] + " ");
			}
		}
		System.out.println("]");


		// 3) 최대/최솟값 출력하기
		int max = nums[0];
		int min = nums[0]; 

		for(int i=1; i<nums.length; i++) {
			if(nums[i] > max) {
				max = nums[i];
				// 현재 값이 max보다 크면 해당값을 max(최댓값)으로 설정
				continue;
			}
			if(nums[i] < min) {
				min = nums[i];
			} // 아니면 작다는 뜻이므로 min(최소값)으로 설정
		}
		
		System.out.println("최댓값  : " + max + " , 최솟값 : " + min);
		
		
		// 4) 오름차순 정렬하기
		for(int i=1; i<nums.length; i++) { // 0부터 시작하면 -1 인덱스 값과 비교하게 된다(error).
			int temp = nums[i-1];
			if(nums[i]<temp) {
				nums[i-1] = nums[i];
				nums[i] = temp;
			}
		}
		
		System.out.println("배열의 오름차순 정렬 : ");
		for(int i=0; i<nums.length; i++) {
			System.out.print(nums[i] + " ");
		}
		
		
		sc.close();
	}
}
```
