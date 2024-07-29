# 통상적인 재귀의 잠재적 위험

1. **종료 조건이 없음 또는 잘못된 경우**:
    - 종료 조건이 없으면 재귀 호출이 무한히 계속되어 스택 오버플로(Stack Overflow) 오류가 발생합니다.
    - 예를 들어, 팩토리얼 함수에서 종료 조건 없이 계속 호출하면 스택이 무한히 증가합니다.
2. **잘못된 값을 반환하거나 반환을 잊는 경우**:
    - 올바른 종료 조건이 있더라도 잘못된 값을 반환하면 재귀 호출이 끝나지 않습니다.
    - 예를 들어, `return num * factorial(num)`으로 작성하면 종료 조건에 도달하지 못하고 무한히 반복됩니다.
    - 반환을 잊으면 호출 스택에서 호출을 지우지 않기 때문에 스택이 계속 쌓입니다.
3. **콘솔 로그 사용 문제**:
    - 종료 조건에 도달했더라도 `return` 대신 `console.log`를 사용하면 호출 스택이 지워지지 않습니다.
    - 예를 들어, `return 1` 대신 `console.log(1)`을 사용하면 스택이 계속 증가합니다.

**핵심 내용**:

- 종료 조건을 명확히 설정해야 하며, 잘못된 값을 반환하지 않도록 주의해야 합니다.
- 반환을 잊지 않아야 하며, 콘솔 로그를 반환으로 대체해야 합니다.
- 스택 오버플로는 재귀 호출이 무한히 계속될 때 발생하며, 이를 방지하려면 올바른 종료 조건과 반환을 사용해야 합니다.

# 헬퍼 메소드 재귀

```jsx
function collectOddValues(arr){
    
    let result = [];

    function helper(helperInput){
        if(helperInput.length === 0) {
            return;
        }
        
        if(helperInput[0] % 2 !== 0){
            result.push(helperInput[0])
        }
        
        helper(helperInput.slice(1))
    }
    
    helper(arr)

    return result;
}

collectOddValues([1,2,3,4,5,6,7,8,9])

//재귀하면서 나오는 return 값을 덮어쓰기 말고 유지한채 업데이트가 되려면
//재귀함수를 감싸는 함수가 있어야하고 변수도 재귀함수의 외부에 있어야함
```

# 순수 재귀

```jsx
function collectOddValues(arr){
    let newArr = [];
    
    //내부 로직 - 1
    if(arr.length === 0) {
        return newArr;
    }
    //내부 로직 - 2
    if(arr[0] % 2 !== 0){
        newArr.push(arr[0]);
    }
    
    //재귀
    newArr = newArr.concat(collectOddValues(arr.slice(1)));
    // [1,2] = [1] + [2]
    // 재귀해서 나온 newArr와 기존 newArr를 concat으로 합치기
    return newArr;
}

collectOddValues([1,2,3,4,5])
```

# 예제 코드

```jsx
function factorial(num){
    if(num === 1) return 1;
    return num * factorial(num-1);
```

```jsx
function sumRange(num){
   if(num === 1) return 1; 
   return num + sumRange(num-1);
}

sumRange(4)
```


```jsx
function countDown(num){
    if(num <= 0) {
        console.log("All done!");
        return;
    }
    console.log(num);
    num--;
    countDown(num);
}
countDown(3)
```