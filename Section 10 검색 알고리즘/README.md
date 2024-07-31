

# 선형 검색 (Linear Search)

- **정의**: 배열의 처음부터 끝까지 하나씩 확인하며 찾는 값이 있는지 검사하는 방법.
- **과정**:
    1. 배열의 첫 번째 요소부터 시작.
    2. 현재 요소가 찾는 값과 일치하는지 확인.
    3. 일치하면 인덱스나 `true`를 반환.
    4. 끝까지 일치하는 값을 찾지 못하면 `1` 또는 `false`를 반환.
- **자바스크립트 내장 메소드**: `indexOf`, `includes`, `find`, `findIndex` 등이 선형 검색을 기반으로 동작.

### 예제 코드 (의사코드)

```
function linearSearch(array, value):
    for i from 0 to length(array) - 1:
        if array[i] == value:
            return i
    return -1

```

- **설명**:
    - `linearSearch` 함수는 배열 `array`와 찾고자 하는 값 `value`를 인수로 받음.
    - 배열의 각 요소를 순차적으로 확인하여 값이 일치하면 해당 인덱스를 반환.
    - 값이 없으면 `1`을 반환.

### 활용 예시

- 사용자명 목록에서 특정 사용자명을 찾을 때 사용.
- 주 또는 영토 목록에서 특정 항목이 존재하는지 확인할 때 사용.

### 검색의 중요성

- **간단하고 효과적인 방법**: 특히 배열이 크지 않을 때 유용.
- **알고리즘 이해**: 기본적인 검색 알고리즘을 이해함으로써 더 복잡한 알고리즘을 학습하는 데 기초가 됨.

### 추가 정보

- **비교 대상**: 정렬된 배열의 경우 이진 검색(Binary Search)이 더 효율적일 수 있음.
- **자바스크립트 예제**:
    
    ```jsx
    const usernames = ['alice', 'bob', 'charlie', 'dave'];
    console.log(usernames.indexOf('charlie')); // 2
    console.log(usernames.includes('eve')); // false
    
    ```
    

```jsx
function linearSearch(arr, val){
    for(var i = 0; i < arr.length; i++){
        if(arr[i] === val) return i;
    }
    return -1;
}

linearSearch([34,51,1,2,3,45,56,687], 100)
```

# 선형 검색 빅오

### 시간 복잡도란?

- **시간 복잡도**는 알고리즘의 성능을 평가하는 척도로, 입력 크기에 따른 실행 시간을 나타냅니다.
- **Big O 표기법**은 가장 높은 차수를 사용하여 시간 복잡도를 간단하게 나타냅니다.

### 선형 검색의 시간 복잡도

- **최선의 경우 (Best Case)**: O(1)
    - 찾고자 하는 값이 배열의 첫 번째 요소인 경우.
- **최악의 경우 (Worst Case)**: O(n)
    - 배열의 마지막 요소 또는 배열에 없는 값을 찾는 경우.
    - n은 배열의 길이입니다.
- **평균의 경우 (Average Case)**: O(n)
    - 모든 요소가 동일한 확률로 검색 대상이 될 때, 평균적으로 배열의 절반을 검색하게 됩니다.
    - Big O 표기법에서는 평균적인 경우도 O(n)으로 나타냅니다.

### 예시를 통한 이해

- **최선의 경우**: 배열 `[1, 2, 3, 4, 5]`에서 1을 찾는 경우, 첫 번째 요소에서 바로 찾음.
    
    ```
    function linearSearch(array, value):
        if array[0] == value:
            return 0
    
    ```
    
- **최악의 경우**: 배열 `[1, 2, 3, 4, 5]`에서 5를 찾거나, 6을 찾는 경우, 모든 요소를 확인해야 함.
    
    ```
    function linearSearch(array, value):
        for i from 0 to length(array) - 1:
            if array[i] == value:
                return i
        return -1
    
    ```
    
- **평균의 경우**: 배열 `[1, 2, 3, 4, 5]`에서 3을 찾는 경우, 배열의 절반을 검색하게 됨.

### Big O 표기법 요약

- O(1): 일정한 시간 내에 완료. (상수 시간)
- O(n): 입력 크기 n에 비례하여 시간이 증가. (선형 시간)
- O(log n): 입력 크기 n에 대해 로그 시간만큼 증가. (로그 시간)
- O(n^2): 입력 크기 n의 제곱에 비례하여 시간이 증가. (제곱 시간)

### 결론

- 선형 검색은 데이터가 정렬되지 않았을 때 가장 간단하고 효율적인 검색 방법입니다.
- 하지만 입력 크기가 클수록 검색 시간이 선형적으로 증가하므로, 더 효율적인 검색 방법이 필요할 수 있습니다.

# 이진 검색 소개

### 이진 검색의 개념

- **정렬된 배열**에서만 사용 가능.
- 매 단계마다 배열을 반으로 나눠가며 값을 찾음.
- 목표 값과 중간 값을 비교하여 검색 범위를 좁혀 나감.

### 이진 검색의 과정

1. **중간점 선택**: 배열의 중간 인덱스를 선택.
2. **값 비교**: 목표 값이 중간 값보다 작은지, 큰지, 같은지 확인.
3. **범위 축소**:
    - 목표 값이 중간 값보다 작으면 왼쪽 절반만 남김.
    - 목표 값이 중간 값보다 크면 오른쪽 절반만 남김.
4. **반복**: 남은 절반에서 다시 중간점을 찾아 같은 과정을 반복.
5. **종료**: 목표 값을 찾으면 해당 인덱스를 반환하고, 끝까지 찾지 못하면 `1` 반환.

### 이진 검색의 시간 복잡도

- **최선의 경우 (Best Case)**: O(1)
    - 첫 번째 비교에서 값을 찾는 경우.
- **최악의 경우 (Worst Case)**: O(log n)
    - n은 배열의 길이. 배열을 반씩 나누기 때문에 로그 시간이 소요됨.
- **평균의 경우 (Average Case)**: O(log n)
    - 최악의 경우와 동일하게 O(log n).

### 예시를 통한 이해

- 배열 `[1, 3, 5, 7, 9, 11, 13, 15, 17, 19]`에서 15를 찾는 경우:
    1. **초기 상태**: 좌측 = 0, 우측 = 9, 중간 = (0 + 9) / 2 = 4 (올림)
    2. **첫 번째 비교**: 중간 값 9와 15 비교 (15 > 9)
        - 새로운 좌측 = 5, 우측 = 9
    3. **두 번째 비교**: 새로운 중간 = (5 + 9) / 2 = 7 (올림)
        - 중간 값 15와 15 비교 (15 == 15)
    4. **값 찾음**: 인덱스 7 반환

### 의사코드 (Pseudocode)

```
function binarySearch(array, value):
    left = 0
    right = length(array) - 1

    while left <= right:
        mid = floor((left + right) / 2)

        if array[mid] == value:
            return mid
        else if array[mid] < value:
            left = mid + 1
        else:
            right = mid - 1

    return -1
```

### 이진 검색의 장점

- 큰 배열에서도 매우 빠른 검색 가능.
- 선형 검색에 비해 효율적이며 시간 절약 가능.

### 결론

- 이진 검색은 데이터가 정렬된 상태에서 매우 효과적인 알고리즘입니다.
- O(log n)의 시간 복잡도로 큰 데이터셋에서도 빠르게 값을 찾을 수 있습니다.
- 다음 단계로는 이진 검색의 시간 복잡도와 Big O 표기법을 자세히 다루겠습니다.

# 이진 검색 의사코드

### 의사코드 (Pseudocode)

> 올바른 방향을 보여주는 것이 의사코드의 목적
> 

> 변수 두개 : 포인터(계산을 시작하는 좌측 인덱스, 배열의 끝인 우측 포인터)
> 

> 반복의 조건 : 항목을 찾았는지? , 좌측 포인터가 우측 포인터보다 앞에 있는지?
> 

### 자바스크립트 코드

```jsx
function binarySearch(array, value) {
    let left = 0;
    let right = array.length - 1;

    while (left <= right) {
        let mid = Math.floor((left + right) / 2);

        if (array[mid] === value) {
            return mid;  // 값 찾음
        } else if (array[mid] < value) {
            left = mid + 1;  // 좌측 포인터 이동
        } else {
            right = mid - 1;  // 우측 포인터 이동
        }
    }

    return -1;  // 값을 찾지 못한 경우
}

// 예시 사용
const sortedArray = [1, 3, 5, 7, 9, 11, 13, 15, 17, 19];
let valueToFind = 15;
let result = binarySearch(sortedArray, valueToFind);
console.log(`Value ${valueToFind} found at index: ${result}`);

valueToFind = 20;
result = binarySearch(sortedArray, valueToFind);
console.log(`Value ${valueToFind} not found, function returned: ${result}`);

```

### 동작 원리 설명

1. **초기화**:
    - `left` 포인터는 배열의 시작 인덱스 (`0`)로 설정.
    - `right` 포인터는 배열의 마지막 인덱스 (`len(array) - 1`)로 설정.
2. **반복 조건**: `while left <= right`
    - `left` 포인터가 `right` 포인터보다 크지 않은 동안 반복.
3. **중간점 계산**: `mid = (left + right) // 2`
    - 현재 `left`와 `right`의 중간 인덱스를 계산.
4. **값 비교**:
    - **같은 경우**: `array[mid] == value`
        - 값을 찾았으므로 `mid` 인덱스를 반환.
    - **작은 경우**: `array[mid] < value`
        - 값이 중간점보다 크므로, `left` 포인터를 `mid + 1`로 이동.
    - **큰 경우**: `array[mid] > value`
        - 값이 중간점보다 작으므로, `right` 포인터를 `mid - 1`로 이동.
5. **값을 찾지 못한 경우**: `return -1`
    - 반복이 끝나고도 값을 찾지 못하면 `1`을 반환.

### 예시 설명

- 정렬된 배열 `[1, 3, 5, 7, 9, 11, 13, 15, 17, 19]`에서 `15`를 찾는 경우:
    - 중간점 `9`와 비교 → `15 > 9`이므로 `left` 포인터 이동.
    - 새로운 중간점 `17`과 비교 → `15 < 17`이므로 `right` 포인터 이동.
    - 새로운 중간점 `15`와 비교 → 값 찾음, 인덱스 `7` 반환.
- 배열에 없는 값 `20`을 찾는 경우:
    - 중간점 `9`와 비교 → `20 > 9`이므로 `left` 포인터 이동.
    - 새로운 중간점 `17`과 비교 → `20 > 17`이므로 `left` 포인터 이동.
    - 남은 부분을 계속 비교하다가 `left > right`가 되면 `1` 반환.

# 이진 검색 (Binary Search) 코드 설명

### 오리지널 솔루션

```jsx
function binarySearch(arr, elem) {
    var start = 0;
    var end = arr.length - 1;
    var middle = Math.floor((start + end) / 2);
    while(arr[middle] !== elem && start <= end) {
        if(elem < arr[middle]){
            end = middle - 1;
        } else {
            start = middle + 1;
        }
        middle = Math.floor((start + end) / 2);
    }
    if(arr[middle] === elem){
        return middle;
    }
    return -1;
}
```

**변수 초기화**:

- `start`는 배열의 시작 인덱스 (`0`)로 초기화됩니다.
- `end`는 배열의 마지막 인덱스 (`arr.length - 1`)로 초기화됩니다.
- `middle`은 `start`와 `end`의 중간 인덱스 (`Math.floor((start + end) / 2)`)로 초기화됩니다.

**반복문 (while loop)**:

- 조건: `arr[middle]`이 `elem`과 같지 않고 `start`가 `end`보다 작거나 같을 때까지 반복합니다.
- **중간 값 비교**:
    - `elem`이 `arr[middle]`보다 작으면:
        - `end`를 `middle - 1`로 업데이트합니다.
    - `elem`이 `arr[middle]`보다 크면:
        - `start`를 `middle + 1`로 업데이트합니다.
- **중간 인덱스를 업데이트합니다**: `middle = Math.floor((start + end) / 2)`.

**결과 반환**:

- 반복문이 종료된 후, `arr[middle]`이 `elem`과 같으면 `middle`을 반환합니다.
- 그렇지 않으면 `1`을 반환합니다.

### 리팩토링된 버전

```
function binarySearch(arr, elem) {
    var start = 0;
    var end = arr.length - 1;
    var middle = Math.floor((start + end) / 2);
    while(arr[middle] !== elem && start <= end) {
        if(elem < arr[middle]) end = middle - 1;
        else start = middle + 1;
        middle = Math.floor((start + end) / 2);
    }
    return arr[middle] === elem ? middle : -1;
}

```

- `if-else` 블록의 중괄호 `{}`를 생략하여 코드가 더 간결해졌습니다.
- 마지막 `if` 조건을 삼항 연산자 `? :`를 사용하여 한 줄로 줄였습니다.

# 이진 검색 비오

### 시간 복잡도의 개요

- **최선의 경우 (Best Case)**: O(1)
    - 중간점을 선택했을 때 첫 번째 비교에서 값을 찾는 경우.
- **평균적인 경우 (Average Case)** 및 **최악의 경우 (Worst Case)**: O(log n)
    - n은 배열의 길이.
    - 로그 시간 복잡도는 매번 검색 범위를 절반으로 줄이기 때문에 발생.

### 로그 (logarithm) 설명

- *로그 (log)**는 주어진 수가 어떤 밑(base)의 거듭제곱인지를 나타내는 지표입니다.
- 이진 검색에서는 일반적으로 밑이 2인 로그 (log₂)를 사용합니다.
- 예를 들어, log₂ 16 = 4는 2^4 = 16을 의미합니다.

### 로그 기반 시간 복잡도

- n이 16일 때 최대 단계: log₂ 16 = 4
- n이 32일 때 최대 단계: log₂ 32 = 5
- 배열의 길이가 두 배로 늘어날 때마다 단계 수는 1씩 증가합니다.

### Big O 표기법에서 log n의 의미

- **로그 기반 시간 복잡도는 매우 효율적**입니다.
- O(log n)은 **선형 시간 O(n)보다 훨씬 효율적**이며, **큰 데이터셋에서도 빠르게 검색**할 수 있습니다.
- **그래프에서 O(log n)은 선형 시간보다 훨씬 낮은 위치**에 있으며, 큰 데이터셋에서도 거의 일정한 시간 내에 작업을 완료합니다.

### 결론

- **이진 검색의 효율성은 배열이 정렬되어 있을 때만 발휘**됩니다.
- **정렬되지 않은 배열에서는 이진 검색을 사용할 수 없으며, 선형 검색을 사용**해야 합니다.
- **이진 검색의 시간 복잡도는 O(log n)으로, 매우 큰 데이터셋에서도 빠른 검색이 가능**합니다.
- 로그(logarithm)에 대해 더 알고 싶다면 추가적인 자료나 영상을 통해 학습하는 것이 좋습니다.

# 나이브 문자열 검색

> **긴 문자열 내에서 짧은 문자열(부분 문자열)의 등장 횟수를 찾는 기본적인 방법**
> 

> 이 알고리즘은 간단한 방법으로 구현할 수 있지만, 효율성이 떨어질 수 있음
> 

### 알고리즘 설명

1. 긴 문자열에서 짧은 문자열을 검색하는 루프를 작성합니다.
2. 긴 문자열의 각 문자에 대해 짧은 문자열의 각 문자를 비교합니다.
3. 일치하지 않으면 비교를 중단하고 다음 문자로 이동합니다.
4. 짧은 문자열의 모든 문자가 일치하면 카운터를 증가시킵니다.
5. 긴 문자열의 모든 문자를 확인할 때까지 반복합니다.

### 의사코드 (Pseudocode)

1. 함수를 정의합니다: `naiveStringSearch(long, short)`
2. 카운터 변수를 0으로 초기화합니다.
3. **긴 문자열을 반복하는 루프**를 작성합니다.
4. 각 문자에 대해 **짧은 문자열을 반복하는 중첩 루프를 작성**합니다.
5. 문자가 일치하지 않으면 **내부 루프에서 벗어납**니다.
6. **모든 문자가 일치하면 카운터를 증가**시킵니다.
7. 최종적으로 카운터 값을 반환합니다.

# 나이브 문자열 검색 구현

### 자바스크립트 코드

```jsx
function naiveSearch(long, short){
    var count = 0;
    for(var i = 0; i < long.length; i++){
        for(var j = 0; j < short.length; j++){
           if(short[j] !== long[i+j]) break; 
            // 긴 문자열의 현재 위치 i에서 j를 더한 위치와 짧은 문자열의 현재 위치 j를 비교
           if(j === short.length - 1) count++;
           // 짧은 문자열의 끝까지 일치한다면 count를 증가시킴
        }
    }
    return count;
}

naiveSearch("lorie loled", "lol")
```

### 코드 상세 설명

1. **함수 정의 및 초기화**
    - `naiveSearch` 함수는 긴 문자열 `long`과 짧은 문자열 `short`를 인자로 받습니다.
    - `count` 변수를 0으로 초기화하여 `short`가 `long`에 몇 번 나타나는지 셉니다.
2. **외부 루프 (긴 문자열 순회)**
    - `for (var i = 0; i < long.length; i++)`:
        - 긴 문자열 `long`의 각 문자를 순회합니다.
        - `i`는 현재 긴 문자열의 인덱스를 나타냅니다.
3. **내부 루프 (짧은 문자열 순회)**
    - `for (var j = 0; j < short.length; j++)`:
        - 짧은 문자열 `short`의 각 문자를 순회합니다.
        - `j`는 현재 짧은 문자열의 인덱스를 나타냅니다.
4. **문자 비교**
    - `if (short[j] !== long[i + j]) break;`:
        - 긴 문자열의 현재 위치 `i`에서 시작하여 짧은 문자열의 현재 위치 `j`의 문자를 비교합니다.
        - 문자가 일치하지 않으면 내부 루프를 종료하고 다음 `i`로 이동합니다.
5. **일치하는 문자열 확인**
    - `if (j === short.length - 1) count++;`:
        - 짧은 문자열의 끝까지 모두 일치하면, `count`를 증가시킵니다.
        - `j`가 `short.length - 1`이면, 이는 `short`의 모든 문자가 `long`의 해당 부분 문자열과 일치한다는 의미입니다.
6. **결과 반환**
    - `return count;`:
        - 최종적으로 `count` 값을 반환합니다.
        - 이는 긴 문자열에서 짧은 문자열이 몇 번 나타나는지 나타냅니다.
    

### 예제 문자열

- 긴 문자열: `"lorie loled"`
- 짧은 문자열: `"lol"`

### 동작 과정 예시

1. **첫 번째 외부 루프 (i = 0)**
    - `j = 0`: `long[0]` ('l')와 `short[0]` ('l') 비교 → 일치
    - `j = 1`: `long[1]` ('o')와 `short[1]` ('o') 비교 → 일치
    - `j = 2`: `long[2]` ('r')와 `short[2]` ('l') 비교 → 불일치, 내부 루프 종료
2. **두 번째 외부 루프 (i = 1)**
    - `j = 0`: `long[1]` ('o')와 `short[0]` ('l') 비교 → 불일치, 내부 루프 종료
3. **여섯 번째 외부 루프 (i = 6)**
    - `j = 0`: `long[6]` ('l')와 `short[0]` ('l') 비교 → 일치
    - `j = 1`: `long[7]` ('o')와 `short[1]` ('o') 비교 → 일치
    - `j = 2`: `long[8]` ('l')와 `short[2]` ('l') 비교 → 일치, `count` 증가