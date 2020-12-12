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
B 가 윗면 R 가 밑면 그리고 O가 정면으로 설정하였습니다.

### 코딩 구현.
Class 는 두개로 나누었으며 MovingCube는 큐브를 움직이는 명령이 있고, Step3는 그 외 모든 일을 합니다. 
```
1. 명령어 변환
 -> step-1 하고 step-2 명령어 변환보다 복잡하여 따로 commandChange 메소드로 생성하였습니다.
    step-2 와 마찬가지로 " ' " 가 붙으면 다른 명령이 되므로 우선 '이 나온다면 이전 문자와 붙입니다.
    여기서 step-2와는 다르게 뒤에 2라는 숫자가 있습니다. 이는 이전 명령어를 한번 더 실행하는 것입니다.
    U'2를 입력받으면 U 와 ' 을 합칩니다. 그러면 " U' ", " ' ", " 2 " 이렇게 나뉘어집니다.
    따라서 2가 나왔을 때 앞에 '만 있어서 이전 명령어를 다시 실행하는 것이 불가하므로 " ' " 을 제거해줍니다.

    배열에서 특정 문자를 제거하는 법은 우선 리스트로 변환해주고 remove를 사용하여 제거하고 다시 배열로 바꿔줍니다.
    List<String> list = new ArrayList<>(Arrays.asList(shell));
    while (cnt1 !=0) {
        list.remove("'");
        cnt1 --;
    }
    shell = list.toArray(new String[list.size()]);
    여기서 while문을 사용한 이유는 '를 여러번 지워줘야할 때가 있으므로 '의 수 만큼 cnt1을 증가시킨 후
    cnt1 만큼 지워줍니다. 

2. 큐브 움직임 조작
 -> 큐브를 움직이는 것은 MovingCube 클라스에 동작별로 나눴습니다. 

3. 큐브 면 회전. 
 -> 3차원 큐브 는 동작을 하면 어느 한면은 꼭 회전을 합니다. 그러므로 반시계방향, 시계방향 회전
    메소드를 각각 leftRotate, rightRotate로 설정하였습니다. 

4. 조작 받은 명령의 갯수 출력.
 -> finalcount 라는 변수를 만들고 조작을 할때마다 1씩 증가시켜줍니다.
    종료시에 finalcount 같이 출력합니다.
```
### 요구사항

-처음 시작하면 초기 상태를 출력한다.

-간단한 프롬프트 (CLI에서 키보드 입력받기 전에 표시해주는 간단한 글자들 - 예: CUBE> )를 표시해 준다.

-한 번에 여러 문자를 입력받은 경우 순서대로 처리해서 매 과정을 화면에 출력한다.

### 추가 구현 기능.
```
1. 프로그램 종료 시 경과 시간 출력 
 -> Step3에 main을 실행하면 System.currentTimeMillis();을 사용하여 시간을 한번받고
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