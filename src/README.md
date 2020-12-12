## Step-3 _ 루빅스 큐브 구현하기

### 3 X 3 X 3 큐브를 2차원 배열로 아래와 같이 표현하였습니다.
 큐브의 초기 상태 
                
                B B B  
                B B B
                B B B
          W W W O O O G G G Y Y Y
          W W W O O O G G G Y Y Y
          W W W O O O G G G Y Y Y
                R R R
                R R R
                R R R
B 가 윗면 R 가 밑 그리고 O가 정면으로 설정하였습니다.

### 코딩 구현.
```
1. Class 는 두개로 나누었으며 MovingCube는 큐브를 움직이는 명령이 있고, Main에는 그 외 모든 일을 합니다.. 
```
### 요구사항

-처음 시작하면 초기 상태를 출력한다.

-간단한 프롬프트 (CLI에서 키보드 입력받기 전에 표시해주는 간단한 글자들 - 예: CUBE> )를 표시해 준다.

-한 번에 여러 문자를 입력받은 경우 순서대로 처리해서 매 과정을 화면에 출력한다.

### 추가 구현 기능.
```
1. 프로그램 종료 시 경과 시간 출력 
 -> Main에 main을 실행하면 System.currentTimeMillis();을 사용하여 시간을 한번받고
    Q로 종료했을 때나 큐브의 모든 면을 맞추었을 때 다시한번 시간을 가져온다.
    그 후 두 시간 의 차이를 경과 시간으로 출력합니다.
    long min = (afterTime - beforeTime)/60000; // 분
    long sec = (afterTime - beforeTime)/1000;  // 초

2. 큐브의 무작위 섞기 기능
 -> 프롬프트에서 명령어를 random 입력시 명령어를 무작위로 1~10개 반환하여
    실행합니다.
        String[] arr={"F", "F'", "R", "R'", "U", "U'", "B", "B'", "L", "L'", "D", "D'"};
        Random r=new Random();
        int randomValue = (int) (Math.random() * 10 +1);
        String randomCommand = "";
        for (int i=0; i<randomValue; i++){
            randomCommand = randomCommand + arr[r.nextInt(arr.length)];
        }
        return randomCommand;

3. 모든 면을 맞추면 축하 메시지와 함께 프로그램을 자동 종료
 -> 큐브를 움직일 때마다 compare 메소드 실행하여 처음 (origin)과 현재 큐브를 비교합니다.
    비교시작전 숫자 0을 하나 생성합니다. for문으로 문자 하나하나 비교할 때 서로 같다면 1을 더해줍니다.
    for문이 끝나면 숫자를 반환합니다. 
    제 코드는 큐브를 2차원 배열로 설정하였고 빈공간이 있기때문에 총 72개의
    문자가 있습니다. 따라서 숫자가 72일 때  모든 면이 맞다는 의미로 
    반환된 숫자가 72라면 프로그램을 종료합니다 .
```