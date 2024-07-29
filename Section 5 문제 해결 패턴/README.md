# 빈도수 세기 패턴

**[방법]**

- 첫번째 배열에 루프적용
- 두번째 배열의 하위 루프에서 값을 확인

```jsx
function same (arr1, arr2){
		if(arr1.length !== arr2.length){
			return false;
		}
		for(let i = 0; i<arr1.length; i++){
			let correctIndex = arr2.**indexOf**(arr[i] ** 2)
			if(conrrectIndex === -1){
				return false;
			}
				arr2.splice(correctIndex,1)
			}
			return true;
}
```

접근법 : 제곱시간이 사용되기 때문에 순진한 접근법이라고 불림

indexOf : 전체 배열을 반복 or 중첩된 루프의 전체 배열을 잠재적으로 반복

⇒ 배열의 길이를 늘리면 이 값이 증가하여 2차 관계로 중첩됨 ⇒ 중첩된 루프는 되도록 사용하지 않기

### 빈도 카운터 패턴 사용

**[방법]**

- 각 배열에 한번씩 개별적으로 루프를 적용

> 두 개의 루프가 두 개의 중첩된 개별 루프보다 훨씬 나음  ⇒ 선형 시간
> 

```jsx
same([1,2,3,2], [9,1,4,4]);

function same(arr1, arr2){
		if(arr1.length !== arr2.length){
			return false;
		}
		
		// 두 객체를 이용해 각 배열의 개별값의 빈도를 셈
		let frequencyCounter1 = {}
		let frequencyCounter2 = {}
		
		//개별 루프 
		for(let val of arr1){
				frequencyCounter1[val] = ( frequencyCounter1[val] || 0 ) + 1
		}
		
		for(let val of arr2){
				frequencyCounter2 [val] = ( frequencyCounter2 [val] || 0 ) + 1
		}
		
		for(let key in frequencyCounter1){
				if(!(key ** 2 in frequencyCounter2 )){
						return false
				}
				if(frequencyCounter2 [key ** 2] !== frequencyCounter1 [key] ){
						return false
				}
		 }
		return false
}
```

**결과**

```jsx
{1 : 1,  2 : 2,  3 : 1 } => key값은 숫자 / value는 숫자의 빈도수
{1 : 1,  4 : 2,  9 : 1 }
true
```

```jsx
for(let val of arr1){
    // frequencyCounter1[val]가 이미 존재하면 해당 값을 사용하고, 
    // 존재하지 않으면 0을 사용하여 1을 더합니다.
    frequencyCounter1[val] = (frequencyCounter1[val] || 0) + 1;
    // 예: val이 2라면,
    // 첫 번째 반복: frequencyCounter1[2]는 undefined이므로, (undefined || 0) + 1 => 1
    // 두 번째 반복: frequencyCounter1[2]는 1이므로, (1 || 0) + 1 => 2
}

```

```jsx
	for(let key in frequencyCounter1){
				if(!(key ** 2 in frequencyCounter2 )){ 
				// frequencyCounter1의 key ** 2가 frequencyCounter2 객체의 키로 존재하는지 확인
						return false
				}
				if(frequencyCounter2 [key ** 2] !== frequencyCounter1 [key] ){
				// frequencyCounter2[(frequencyCounter1의)key ** 2]와 frequencyCounter1[key]의 값을 비교
				// { 9 : 1 }     /   { 3 : 1 }
						return false
				}
		 }
```

# 다중 포인터 패턴

> 인덱스나 위치에 해당하는 포인터나 값을 만든 다음 특정 조건에 따라 중간 지점에서부터 시작 지점이나 끝 지점이나 양쪽 지점을 향해 이동시키는 것
> 

> 선형 구조, 이중 연결 구조, 이중 연결 리스트, 단일 연결 리스트를 만드는 방법
> 

> 한 쌍의 값이나 조건을 충족시키는 무언가를 찾는 개념임
> 

```jsx
참조값 i 이동 방향=>                   <= 참조값 j 이동 방향
								[-4, -3, -2, -1, 0, 1, 2, 5]

```

**ex)** 

오름차순으로 정렬된 배열을 파라미터로 받는 함수

두개의 포인터 값의 합이 0이여야함

```jsx
sumZero([-3,-2,-1,0,1,2,3]);
```

> 우선 받는 배열이 무조건 정렬되어있어야 효율적인 해결책을 마련할 수 있음
> 

1. **루프 두개 사용**

```jsx
fuction sumZero(arr){
		for(let i = 0; i < arr.length; i++){
			for(let j = i+1; j < arr.length; j++){
				if(arr[i] + arr[j] === 0){
					return [arr[i], arr[j]];
				}
			}
		}
	}
```

1. **리팩토링 ⇒ 시간 복잡도 선형** 

```jsx
fuction sumZero(arr){
		let left = 0;
		let right = arr.length - 1;
		while(left < right){
				let sum = arr[left] + arr[right];
				if(sum === 0){
						return [arr[left], arr[right]];
				}else if(sum > 0){
						right--;
				}else{
						left++;
				}
		}
	}
```

# 기준점 간 이동 배열 패턴

> 배열이나 문자열과 같은 일련의 데이터를 입력하거나 특정 방식으로 연속적인 해당 데이터의 하위 집합을 찾는 경우에 유용
> 

ex ) 긴 시퀀스의 고유 문자를 찾는 함수를 작성
```jsx
"hellothere"
=> 이 경우, l이 두번 나오니 시퀀스가 끊겨짐 
```