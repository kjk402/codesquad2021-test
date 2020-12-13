## Step-2 _ 2 차원 큐브

### 3 X 3의 2차원 배열이 아래처럼 있다.

```
R R W
G C W
G B B
```


### 사용자 입력을 받아서 아래의 동작을 하는 프로그램을 구현하시오
```
> U  가장 윗줄을 왼쪽으로 한 칸 밀기 RRW -> RWR
> U' 가장 윗줄을 오른쪽으로 한 칸 밀기 RRW -> WRR
> R  가장 오른쪽 줄을 위로 한 칸 밀기 WWB -> WBW
> R' 가장 오른쪽 줄을 아래로 한 칸 밀기 WWB -> BWW
> L  가장 왼쪽 줄을 아래로 한 칸 밀기 RGG -> GRG (L의 경우 R과 방향이 반대임을 주의한다.)
> L' 가장 왼쪽 줄을 위로 한 칸 밀기 RGG -> GGR
> B  가장 아랫줄을 오른쪽으로 한 칸 밀기 GBB -> BGB (B의 경우도 U와 방향이 반대임을 주의한다.)
> B' 가장 아랫줄을 왼쪽으로 한 칸 밀기 GBB -> BBG
> Q  Bye~를 출력하고 프로그램을 종료한다.
```
### 코딩 구현.

1. 명령어 변환 

 -> step-2의 명령어는 step-1의 command와는 다르게 문자로만 이루어져 있습니다. 문자와 특수문자 " ' " 가 붙어있다면
 다른 명령이됩니다. 
 따라서 split으로 나누었을 때 '을 처리해주어야합니다. 저는 for문을 사용하여 '이 나온다면 이전 문자와 합치는 방식으로
 구현하였습니다. 
 
        
        String[] shell = command.split("");
        for (int t = 0; t<command.length(); t++) {
             if (shell[t].equals("'")) {
                 shell[t-1] = shell[t-1]+shell[t];
             }
        }

2 동작 메소드

 -> 2차원 큐브의 움직임은 4가지로 나뉩니다. 왼쪽or오른쪽으로 밀기, 위or아래로 밀기.
    각각 메소드를 left/right, up/down으로 생성하였습니다.
    명령어 별로 새로운 메소드를 만들지 않고 미는 위치만 다르고 같은 동작을 하는 명령은 동일 메소드를 사용할 수 있게 하였습니다.
    
    private static String[][] left(Integer num, String[][] arr) {
            String temp = arr[num][0];
            for (int i=1; i<3; i++) {
                arr[num][i-1] =arr[num][i];
            }
            arr[num][2] = temp;
            return arr;
        }
    예를 들어 U 명령어는 가장 윗줄을 왼쪽으로 밀고 B' 명령어는 가장 아랫줄을 왼쪽으로 밉니다.
    3X3 2차원 배열에서 가장 윗줄은 [0][i] 이고 가장 아랫줄은 [2][i]입니다. 
    따라서 U 명령어는 left(0,cube);  // B'명령어는 left(2,cube)를 사용합니다. 


    
    
        
    