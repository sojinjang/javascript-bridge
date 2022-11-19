1. UI 담당 로직
    1) "다리 건너기 게임을 시작합니다." 출력
    2) "다리의 길이를 입력해주세요." 출력
        1) 예외 상황 시 "[ERROR] 다리 길이는 3부터 20 사이의 숫자여야 합니다." 던지기
    3) "이동할 칸을 선택해주세요. (위: U, 아래: D)" 출력
        1) 예외 상황 시 "[ERROR] 이동할 칸은 U 혹은 D만 입력 가능합니다." 던지기
    4) 다리 그리기 
        1) 생성 규칙에 따라 다리 섹션 표시 ([], |)
        2) 성공 / 실패 여부에 따라 해당하는 위치에 O나 X 표시
        3) 현재까지 건넌 다리 모두 출력
    5) 다리 건너기 실패 or 끝까지 건너기 성공
        1) 건너기 실패한 경우
            1) "게임을 다시 시도할지 여부를 입력해주세요. (재시도: R, 종료: Q)" 출력
            2) 예외 상황 시 "[ERROR] 재시도 여부는 R 혹은 Q만 입력 가능합니다." 던지기
            3) 재시도 선택
                1) 현재까지 건넌 다리 초기화한 뒤 iii.부터 다시 호출됨
            4) 종료 선택
                1) "최종 게임 결과" 출력
                2) 건넌 다리 모양 출력
                3) "게임 성공 여부: 실패" 출력
                4) "총 시도한 횟수: ${모든 시도 포함한 총 시도 횟수}" 출력
        2) 끝까지 건넌 경우 
            1) "최종 게임 결과" 출력
            2) 건넌 다리 모양 출력
            3) "게임 성공 여부: 성공" 출력
            4) "총 시도한 횟수: ${모든 시도 포함한 총 시도 횟수}" 출력

2. 핵심 로직 
    1) 다리 길이 입력 받기
        1) 예외 상황 시 ERROR 출력 UI 로직 호출
    2) 다리 생성
        1) 길이가 입력받은 다리 길이인 0 또는 1로 이루어진 정답 다리 리스트 생성
        2) 0은 D로, 1은 U로 replace
    3) 이동할 칸 입력 받기
        1) 예외 상황 시 ERROR 출력 UI 로직 호출
        2) U를 선택한 경우 -> 정답 다리 리스트 해당 칸이 U인 경우 통과, D인 경우 실패
        3) D를 선택한 경우 -> 정답 다리 리스트 해당 칸이 D인 경우 통과, U인 경우 실패
        4) 통과 혹은 실패 여부 UI 로직에 넘겨주기
    4) 다리 건너기 실패 or 끝까지 건너기 성공할때까지 iii. 반복
    5) 다리 건너기 실패 or 성공
        1) 건너기 실패한 경우 재시도 여부 입력 받기
            1) 예외 상황 시 ERROR 출력 UI 로직 호출
            2) 재시도 선택
                1) 처음에 만든 정답 다리 리스트, 총 시도 횟수 기억한채로 iii.으로 다시 돌아감
            3) 종료 선택
                1) 최종 게임 결과 출력 메서드 호출
                2) 총 시도 횟수 UI 로직에 넘겨주기
        2) 끝까지 건넌 경우
            1) 최종 게임 결과 출력 메서드 호출
            2) 총 시도 횟수 UI 로직에 넘겨주기