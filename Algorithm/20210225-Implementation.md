## :star: Implementation (Reference : 이것이 코딩테스트다.)

### 1. 아이디어를 코드로 바꾸는 구현
- 코딩 테스트에서 구현이란 **머릿속에 있는 알고리즘을 소스코드로 바꾸는 과정**이다. 어떤 문제를 풀든 간에 소스코드를 작성하는 과정은 필수이므로 구현 문제 유형은 모든 범위의 코딩 테스트 문제 유형을 포함하는 개념이다.
- Problem -> Thinking -> Solution
- 흔히 문제 해결 분야에서 구현 유형의 문제는 **풀이를 떠올리는 것은 쉽지만 소스코드로 옮기기 어려운 문제**를 의미한다.
- **완전 탐색**은 **모든 경우의 수를 주저 없이 다 계산하는 해결 방법**을 의미하고, **시뮬레이션**은 **문제에서 제시한 알고리즘을 한 단계씩 차례대로 직접 수행**해야 하는 문제 유형을 의미한다.
- 코딩 테스트 수준에서는 메모리 사용량 제한보다 더 적은 크기의 메모리를 사용해야 한다는 점 정도만 기억하자.

### :speech_balloon: 상하좌우

```
여행가 A는 N x N 크기의 정사각형 공간 위에 서 있다. 이 공간은 1 x 1 크기의 정사각형으로 나누어져 있다.
가장 왼쪽 위 좌표는 (1, 1)이며, 가장 오른쪽 아래 좌표는 (N, N)에 해당한다.
여행가 A는 상, 하, 좌, 우 방향으로 이동할 수 있으며, 시작 좌표는 항상 (1, 1)이다.
우리 앞에는 여행가 A가 이동할 계획이 적힌 계획서가 놓여 있다.
계획서에는 하나의 줄에 띄어쓰기를 기준으로 하여 L, R, U, D 중 하나의 문자가 반복적으로 적혀있다.
각 문자의 의미는 다음과 같다.
    - L : 왼쪽으로 한 칸 이동
    - R : 오른쪽으로 한 칸 이동
    - U : 위로 한 칸 이동
    - D : 아래로 한 칸 이동
이때 여행가 A가 N x N 크기의 정사각형 공간을 벗어나는 움직임은 무시된다.
예를 들어 (1, 1)의 위치에서 L 혹은 U를 만나면 무시된다.
```

### :computer: Code

```
N = int(input())
count = [1, 1]
String = list(map(str, input().split()))

for i in range(len(String)):
    if String[i]=='U':
        if (count[0]-1)==0:
            continue
        else:
            count[0] -= 1
    elif String[i]=='D':
        if (count[0]+1)==(N+1):
            continue
        else:
            count[0] += 1
    elif String[i]=='L':
        if(count[1]-1)==0:
            continue
        else:
            count[1] -= 1
    else:
        if(count[1]+1)==(N+1):
            continue
        else:
            count[1] += 1

print(*count)
```

```
N = int(input())
count = [1, 1]

String = list(map(str, input().split()))
movetype = ['L', 'R', 'U', 'D']

dx = [0, 0, -1, 1]
dy = [-1, 1, 0, 0]

nx = 0
ny = 0

for x in String:
    for y in range(len(movetype)):
        if x == movetype[y]:
            nx = count[0] + dx[y]
            ny = count[1] + dy[y]
    if nx < 1 or ny < 1:
        continue
    else:
        count[0], count[1] = nx, ny
print(*count)
```

### :pencil2: 문제 해설

```
이 문제를 요구사항대로 구현하면 연산 횟수는 이동 횟수에 비례하게 된다.
예를 들어 이동 횟수가 N번인 경우 시간 복잡도는 O(N)이다. 따라서 이 문제의 시간 복잡도는 매우 넉넉한 편이다.
이러한 문제는 일련의 명령에 따라서 개체를 차례대로 이동시킨다는 점에서 시뮬레이션 유형으로 분류되며 구현이 중요한 대표적인 문제 유형이다.
위의 두 번째 풀이는 책에서 나온 풀이이고, 첫 번째 풀이는 내가 푼 풀이이다. 시간복잡도가 첫 번째 해결 방법이 더 좋다.
```

### :speech_balloon: 시각

```
정수 N이 입력되면 00시 00분 00초부터 N시 59분 59초까지의 모든 시각 중에서 3이 하나라도 포함되는 모든 경우의 수를 구하는 프로그램을 작성하시오.
예를들어 1을 입력했을 때 다음은 3이 하나라도 포함되어 있으므로 세어야 하는 시간이다.
```

### :computer: Code

```
"""
author : Park Min Hyeok
github : https://github.com/m1nnh
e-mail : alsgur9784@naver.com

title : 시각
정수 N이 입력되면 00시 00분 00초부터 N시 59분 59초까지의 모든 시각 중에서 3이 하나라도 포함되는 모든 경우의 수를 구하는 프로그램을 작성하시오.
예를들어 1을 입력했을 때 다음은 3이 하나라도 포함되어 있으므로 세어야 하는 시간이다.
"""

N = int(input())
count = 0
time = [0, 0, 0]
for i in range(N + 1):
    time[1] = 0
    if '3' in str(time[0]):
        count += (60 * 60)
        time[0] += 1
    else:
        for j in range(61):
            time[2] = 0
            if '3' in str(time[1]):
                count += 60
                time[1] += 1
            else:
                if j == 59:
                    time[0] += 1
                else:
                    for k in range(60):
                        if '3' in str(time[2]):
                            count += 1
                            time[2] += 1
                        else:
                            time[2] += 1
                            if k == 59:
                                time[1] += 1
print(count)
```

```
N = int(input())

count = 0
for i in range(N+1):
    for j in range(60):
        for k in range(60):
            if '3' in str(i) + str(j) + str(k):
                count += 1

print(count)
```

### :pencil2: 문제 해설

```
이 문제는 시간 복잡도가 좋지는 않다. 그래서 솔루션 두 번째인 경우는 N이 주어질 때 N-1 : 59 : 59까지 전체를 검사한다.
하지만 첫 번째 솔루션을 보게 되면 시를 가리키는 것이 3이 있을 때 나머지 분과 초는 구해주지 않아도 되기 때문에 3600을 더했고,
분이 3이 있을 때 초를 가리키는 반복문 또한 돌아지 않아도 되기 때문에 바로 60을 더해준다.
시간 복잡도를 조금더 효율적으로 구현하기 위해 솔루션 1과 같이 풀었다.  
```
 
### :speech_balloon: 왕실의 나이트

```
행복 왕국의 왕실 정원은 체스판과 같은 8 x 8 좌표 평면이다. 왕실 정원의 특정한 한 칸에 나이트가 서 있다. 나이트는 매우 충성스러운 신하로서 매일 무술을 연마한다.
나이트는 말을 타고 있기 때문에 이동을 할 때는 L자 형태로만 이동할 수 있으며 정원 밖으로는 나갈 수 없다. 나이트는 특정한 위치에서 다음과 같은 2가지 경우로 이동할 수 있다.
    1. 수평으로 두 칸 이동한 뒤에 수직으로 한 칸 이동하기
    2. 수직으로 두 칸 이동한 뒤에 수평으로 한 칸 이동하기
이처럼 8 x 8 좌표 평면상에서 나이트의 위치가 주어졌을 때 나이트가 이동할 수 있는 경우의 수를 출력하는 프로그램을 작성하시오.
이때 왕실의 정원에서 행 위치를 표현할 때는 1부터 8로 표현하며, 열 위치를 표현할 때는 a부터 h로 표현한다.
```


### :computer: Code

```
now_data = input()

row = int(now_data[1])
column = int(ord(now_data[0]) - ord('a') + 1)

dr = [-2, -2, -1, -1, 1, 1, 2, 2]
dc = [-1, 1, -2, 2, -2, 2, -1, 1]
count = 0

for i in range(8):
    nr = dr[i] + row
    nc = dc[i] + column

    if nr >= 1 and nr <= 8 and nc >= 1 and nc <= 8:
        count += 1

print(count)
```


### :pencil2: 문제 해설

```
이동과 관련 될 때는 미리 이동할 경우의 수를 저장 해두고 검사를 하는 것이 좋다.
```

### :speech_balloon: 게임 개발

```
현민이는 게임 캐릭터가 맵 안에서 움직이는 시스템을 개발 중이다.
캐릭터가 있는 장소는 1 x 1 크기의 정사각형으로 이뤄진 N x M 크기의 직사각형으로, 각각의 칸은 육지 또는 바다이다.
캐릭터는 동서남북 중 한 곳을 바라본다.
맵의 각 칸은 (A, B)로 나타낼 수 있고, A는 북쪽으로부터 떨어진 칸의 개수, B는 서쪽으로부터 떨어진 칸의 개수이다.
캐릭터는 상하좌우로 움직일 수 있고, 바다로 되어 있는 공간에는 갈 수 없다.
캐릭터의 움직임을 설정하기 위해 정해 놓은 매뉴얼은 이러하다.
    1. 현재 위치에서 현재 방향을 기준으로 왼쪽 방향 (반시계 방향으로 90도 회전한 방향)부터 차례대로 갈 곳을 정한다.
    2. 캐릭터의 바로 왼쪽 방향에 아직 가보지 않은 칸이 존재한다면, 왼쪽 방향으로 회전한 다음 왼쪽으로 한 칸을 전진한다.
    왼쪽 방향에 가보지 않은 칸이 없다면, 왼쪽 방향으로 회전만 수행하고 1단계로 돌아간다.
    3. 만약 네 방향 모두 이미 가본 칸이거나 바다로 되어 있는 칸인 경우에는, 바라보는 방향을 유지한 채로 한 칸 뒤로 가고 1단계로 돌아간다.
    단, 이때 뒤쪽 방향이 바다인 칸이라 뒤로 갈 수 없는 경우에는 움직임을 멈춘다.
현민이는 위 과정을 반복적으로 수행하면서 캐릭터의 움직임에 이상이 있는지 테스트하려고 한다.
매뉴얼에 따라 캐릭터를 이동시킨 뒤에, 캐릭터가 방문한 칸의 수를 출력하는 프로그램을 만드시오.
```

### :computer: Code

```
N, M = map(int, input().split())
x, y, d = map(int, input().split())

dx = [-1, 0, 1, 0]
dy = [0, 1, 0, -1]

info = []
for i in range(N):
    info.append(list(map(int, input().split())))

info[x][y] = 1
count = 1
turn = 0

while True:
    if d == 0:
        d = 3
    else:
        d -= 1

    nx = x + dx[d]
    ny = y + dy[d]

    if info[nx][ny] == 0:
        info[nx][ny] = 1
        x = nx
        y = ny
        count += 1
        turn = 0
        continue
    else:
        turn += 1

    if turn == 4:
        nx = x - dx[d]
        ny = y - dy[d]

        if info[nx][ny] == 0:
            x = nx
            y = ny
        else:
            break
        turn = 0

print(count)
```


### :pencil2: 문제 해설

```
이 문제는 전형적인 시뮬레이션 문제이다. 삼성전자 공채 코딩 테스트에서 자주 출제되는 대표적인 유형이기도 하다.
별도의 알고리즘이 필요하기 보다는 문제에서 요구하는 내용을 오류 없이 성실하게 구현만 할 수 있다면 풀 수 있다는 특징이 있다.
```
