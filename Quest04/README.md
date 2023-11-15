# AIFFEL Campus Online Code Peer Review Templete
- 코더 : 조보겸
- 리뷰어 : 강영현


# PRT(Peer Review Template)
- [x]  **1. 주어진 문제를 해결하는 완성된 코드가 제출되었나요?**

    !pip install ColabTurtlePlus # ColabTurtle 라이브러리 설치
from ColabTurtlePlus.Turtle import * # ColabTurtle 라이브러리에서 Turtle 클래스를 import


# 미로 데이터
maze = [
    [0, 1, 0, 0, 0],
    [0, 0, 0, 1, 1],
    [0, 1, 1, 0, 0],
    [0, 0, 1, 1, 0],
    [0, 0, 0, 0, 0]
]

# 시작 위치와 목적지 위치
start_x, start_y = 0, 0
end_x, end_y = 4, 4

# 터틀 초기 설정
window = (100, 100)
initializeTurtle(window, 'logo')
speed(1)

# dx ,dy = 갈 방향 / nx, ny = 다음 위치 / x,y = 현재 위치
# 미로 찾기 알고리즘
def solve_maze(x, y):

  # 목적지에 도착한 경우
  if x == end_x & y == end_y:

      # "미로를 찾았습니다" 라는 문장을 출력하고
      print('미로를 찾았습니다!')

      # True를 반환한다.
      return True

  # 현재 위치에서 갈 수 있는 방향 탐색
  for dx, dy in [(0, 1), (1, 0), (0, -1), (-1, 0)]:
      nx, ny = x + dx, y + dy

      # 미로 범위(0,0 ~ 4,4) 내에 있고, 갈 수 있는 길인 경우
      # and 와 & 차이 : 비트연산자와 논리연산자의 차이
      if start_x <= nx and end_x >= nx and start_y <= ny and end_y >= ny and maze[nx][ny] == 0:


          # 갔던 길 표시
          print('-'*20)
          print('현재 위치 :',nx,ny)
          print('이동하기로 한 방향 : ', dx,dy)
          print('-'*20,'\n')
          maze[nx][ny] = 2

          pendown()
          # 다음 위치로 이동
          goto(nx*10, ny*10)  # 거북이 다음 위치로 이동

          penup()

          # 코드를 해석해주세요!!
          # 최종적으로 목적지에 도달한 경우 조건문이 True가 되어 최종적으로 True 반환
          # 계속해서 재귀호출을 통해 미로 탐색 진행
          if solve_maze(nx, ny):
              return True

          # 막다른 길에 도달한 경우
          else:
              # 다시 이전으로 돌아가기
              pendown()

              goto(x*10, y*10)

              penup()

              print('back :',x,y)

              # 표시된 길 0표시(지우기)

              print('막다른 곳으로 판별된 곳 : ', nx, ny,'\n')

              # 이 부분을 0으로 바꾸면, 이동하는 위치가 무한루프에 갇히는 것 아닌가?
              # 하지만, 이미 for문에서 이 방향에 대한 탐색이 이뤄어졌기 때문에 다시 이 부분으로 돌아가지 않는다.
              maze[nx][ny] = 0

  # 길을 찾지 못한 경우
  # "길을 찾을 수 없습니다"를 출력하고
  # False를 리턴
  print('*'*20)
  print("길을 찾을 수 없습니다.")
  print('*'*20,'\n')
  return False

# 시작 위치에서 미로 찾기 시작
goto(start_x, start_y)
solve_maze(start_x, start_y)
import pprint
pprint.pprint(maze)

    - 문제에서 요구하는 최종 결과물이 첨부되었는지 확인
    - 문제를 해결하는 완성된 코드란 프로젝트 루브릭 3개 중 2개, 
    퀘스트 문제 요구조건 등을 지칭
        - 해당 조건을 만족하는 코드를 캡쳐해 근거로 첨부
    
- [x]  **2. 전체 코드에서 가장 핵심적이거나 가장 복잡하고 이해하기 어려운 부분에 작성된 
주석 또는 doc string을 보고 해당 코드가 잘 이해되었나요?**

    # 계속해서 재귀호출을 통해 미로 탐색 진행
          if solve_maze(nx, ny):
              return True

          # 막다른 길에 도달한 경우
          else:
              # 다시 이전으로 돌아가기
              pendown()

              goto(x*10, y*10)

              penup()

              print('back :',x,y)

              # 표시된 길 0표시(지우기)

              print('막다른 곳으로 판별된 곳 : ', nx, ny,'\n')

              # 이 부분을 0으로 바꾸면, 이동하는 위치가 무한루프에 갇히는 것 아닌가?
              # 하지만, 이미 for문에서 이 방향에 대한 탐색이 이뤄어졌기 때문에 다시 이 부분으로 돌아가지 않는다.
              maze[nx][ny] = 0
       
    - 해당 코드 블럭에 doc string/annotation이 달려 있는지 확인
    - 해당 코드가 무슨 기능을 하는지, 왜 그렇게 짜여진건지, 작동 메커니즘이 뭔지 기술.
    - 주석을 보고 코드 이해가 잘 되었는지 확인
        - 잘 작성되었다고 생각되는 부분을 캡쳐해 근거로 첨부합니다.
        
- [x]  **3. 에러가 난 부분을 디버깅하여 문제를 “해결한 기록을 남겼거나” 
”새로운 시도 또는 추가 실험을 수행”해봤나요?**

    if solve_maze(nx, ny):
              return True

          # 막다른 길에 도달한 경우
          else:
              # 다시 이전으로 돌아가기
              pendown()

              goto(x*10, y*10)

              penup()

              print('back :',x,y)

              # 표시된 길 0표시(지우기)

              print('막다른 곳으로 판별된 곳 : ', nx, ny,'\n')
       
    - 문제 원인 및 해결 과정을 잘 기록하였는지 확인
    - 문제에서 요구하는 조건에 더해 추가적으로 수행한 나만의 시도, 
    실험이 기록되어 있는지 확인
        - 잘 작성되었다고 생각되는 부분을 캡쳐해 근거로 첨부합니다.
        
- [x]  **4. 회고를 잘 작성했나요?**

      ![image](https://github.com/JoBoB1218/AIFFEL_Online_Quest/assets/149550120/b2616b36-e326-49e3-8c0a-2fb65b101608)

    - 주어진 문제를 해결하는 완성된 코드 내지 프로젝트 결과물에 대해
    배운점과 아쉬운점, 느낀점 등이 기록되어 있는지 확인
    - 전체 코드 실행 플로우를 그래프로 그려서 이해를 돕고 있는지 확인
        - 잘 작성되었다고 생각되는 부분을 캡쳐해 근거로 첨부합니다.
        
- [x]  **5. 코드가 간결하고 효율적인가요?**

      if solve_maze(nx, ny):
              return True

          # 막다른 길에 도달한 경우
          else:
              # 다시 이전으로 돌아가기
              pendown()

              goto(x*10, y*10)

              penup()

              print('back :',x,y)

              # 표시된 길 0표시(지우기)

              print('막다른 곳으로 판별된 곳 : ', nx, ny,'\n')

    - 파이썬 스타일 가이드 (PEP8) 를 준수하였는지 확인
    - 하드코딩을 하지않고 함수화, 모듈화가 가능한 부분은 함수를 만들거나 클래스로 짰는지
    - 코드 중복을 최소화하고 범용적으로 사용할 수 있도록 함수화했는지
        - 잘 작성되었다고 생각되는 부분을 캡쳐해 근거로 첨부합니다.


# 참고 링크 및 코드 개선
```
# 코드 리뷰 시 참고한 링크가 있다면 링크와 간략한 설명을 첨부합니다.
# 코드 리뷰를 통해 개선한 코드가 있다면 코드와 간략한 설명을 첨부합니다.
