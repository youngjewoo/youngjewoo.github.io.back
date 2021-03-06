---
layout: post
title:  "[leetcode] Two Sum"
date:   2021-03-11 23:19:54 +0900
categories: jekyll update
---
### Two Sum

[Two Sum - LeetCode](https://leetcode.com/problems/two-sum/)

오늘은 Two Sum 이라는 문제를 풀며 느낌 점을 적어보겠습니다.

해당 문제는 주어진 숫자 배열, 목표값 두 가지 정보가 주어지고,

주어진 숫자 배열에 있는 숫자 '두 개'를 더해서 목표값이 되는 인덱스들을 리턴하는 문제 입니다.

🤠 Ex) nums = [ 1, 2, 3 ] , target = 3                answer : [ 0 , 1 ] 


이 문제를 풀어 나갔던 과정에 대해 적어 보겠습니다.


### 첫 번째 (Brute force)

 첫 번째로는 가장 직관적인 방법을 선택했습니다.

![Untitled](https://user-images.githubusercontent.com/22024761/110954591-05bf1100-838c-11eb-842a-112d58171bba.png)


시간 복잡도 : O(n^2)

공간 복잡도 : O(1)


O(n^2) 이라는 복잡도는 분명 불쾌하게 느껴지지만 문제의 조건상 

주어지는 문자열의 길이가 2~1000 사이로 worst case에 1,000,000번 계산을 수행하지만

꽤 나쁘지 않은 수행시간으로 문제를 통과할 수 있습니다.

더구나 추가적인 메모리도 사용하지 않죠.

실제로 leetcode의 최상의 수행시간에도 별 자료구조를 사용하지 않은 해당 방법이

1등을 차지하고 있습니다.

문제의 run-time 1등 코드

![Untitled (1)](https://user-images.githubusercontent.com/22024761/110954620-0c4d8880-838c-11eb-8218-4a3cffc71420.png)


문제의 메모리 사용량
  
![Untitled (2)](https://user-images.githubusercontent.com/22024761/110954618-0bb4f200-838c-11eb-970b-20fb03ecf69b.png)

메모리 사용량은 1등을 하는 기염을 토합니다.

하지만 누구나 짐작했듯이 주어지는 문자열의 길이가 길어질수록 

TLE(Time limit Error)를 만날 확률이 높아지겠죠.


## 두 번째 (Map을 사용하여 search 시간복잡도를 log(n) 으로)


두 번째 문제를 풀 때 생각난 방법은 Map을 통해 원하는 값을 찾는 시간을 줄이는 것이었습니다.

기존의 배열 순차적 탐색 방식 O(n)

![Untitled (3)](https://user-images.githubusercontent.com/22024761/110954617-0bb4f200-838c-11eb-9414-a460c3824ff6.png)


Map을 이용한 탐색 O(log(n))

![Untitled (4)](https://user-images.githubusercontent.com/22024761/110954615-0b1c5b80-838c-11eb-99b3-f678a0135618.png)

시간 복잡도 : O(n log n)

공간 복잡도 : O(n)

시간 복잡도를 n log n 으로 낮추는 쾌거를 이루어 냈습니다!

(Map에서 찾은 원소가 현재 나와 같은 인덱스인지 검사하는 것을 빼먹어서 Fail이 난 것은 두고두고 기억해야할 것입니다......)

저는 이 정도로 만족했지만 여전히 만족하지 못하고 새로운 방법을 제시하는 사람들이 있더군요.

사실 위 방법에는 한 가지 비효율적인 부분이 있습니다.

이미 검사가 끝난 값도 여전히 Map에 남아 있음

![Untitled (5)](https://user-images.githubusercontent.com/22024761/110954612-0b1c5b80-838c-11eb-974c-c9511275c9c5.png)

배열에서 한 번 검사한 값은 정답이 될 수 없기 때문에 \
더 이상 검사하지 않아도 됩니다.

하지만 여전히 Map에 남아있기 때문에 
다음 원소의 정답 여부를 판별할 때에도 계속 오버헤드를 발생시키게 되죠.

그래서 저는 

"아! 검사가 끝난 원소는 맵에서 제거해주면 되겠구나! "

라고 생각했습니다.

검사가 끝난 원소를 Map에서 제거

![Untitled (6)](https://user-images.githubusercontent.com/22024761/110954610-0a83c500-838c-11eb-856c-78dfb89c9658.png)


캬 이로서 극한의 최적화가 완성됐습니다.

라고 저는 멋지다고 생각했지만,

세상에나 이보다 더 나은 방법이 존재했습니다.

최고의 장수는 싸우지 않고 이기는 장수라 했던가요.

애초에 Map을 다 구성 해놓고 검사를 시작하는 것이 아니라, Map을 구성하면서 검사를 하는 방법이 존재했습니다. 

## 마지막 (검사가 끝난 원소를 Map으로 구성)

검사한 원소를 Map에 집어 넣고 다음 원소를 검사

![Untitled (7)](https://user-images.githubusercontent.com/22024761/110954608-09eb2e80-838c-11eb-94a8-0ad7684e347c.png)


시간 복잡도 : O(n log n)

공간 복잡도 : O(n)

이런식으로 검사해야하는 원소 수를 최적화할 수 있습니다.

(+ Map에 있는 원소가 나와 같은 인덱스의 원소인지 판별하는 로직도 필요 없어 지겠죠)

비록 시간/공간 복잡도 상으로는 동일하지만 누가봐도 더 효율적인 로직임이 분명합니다.

비로소 가장 최적화된 답을 냈다고 할 수 있겠습니다.

Easy 난이도라고 생각해서 처음 공부 시작할 때 Brute force로 풀고 어? 통과했네 ㅋ

하고 넘어갔던 문제인데 다시 보니 생각의 흐름이 배울점이 많은 것 같아서 이렇게

따로 정리해둡니다.
