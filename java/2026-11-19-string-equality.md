# 오늘의 학습 자료 · String 값 비교

String에서 ==는 두 변수가 같은 객체를 참조하는지 확인한다. equals는 문자열 내용을 비교한다.

직접 만든 예제에서 String a = new String("queue"), b = new String("queue")이면 a == b는 false, a.equals(b)는 true다. 명령어 분기는 command.equals("push")처럼 내용으로 비교한다.

핵심 질문. 문자열 리터럴 두 개에서 ==가 true인 결과만 보고 명령 비교에 ==를 쓰면 왜 위험할까?

직접 해볼 연습. 위 두 표현식의 결과를 먼저 예상하고 작은 main에서 출력해 확인한다. null일 수 있는 변수와 비교할 때 "push".equals(command)를 쓰는 이유도 적는다.

복습. 큐 FIFO, 조회와 제거 차이, 입력 명령 처리 흐름을 설명한다.
