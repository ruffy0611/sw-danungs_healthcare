usecaseDiagram
    actor User as "사용자"
    
    rect "AI 기반 스마트 피트니스 및 식단 관리 시스템" {
        usecase UC1 as "실시간 운동 자세 분석 및 화면 표시하기"
        usecase UC2 as "자세 오류 감지 및 1초 이내 피드백 제공하기"
        usecase UC3 as "위험 자세 감지 및 즉시 경고 제공하기"
        usecase UC4 as "동일 근육군 대체 운동 3개 이상 추천받기"
        usecase UC5 as "개인 데이터 기반 운동 강도 및 중량 추천받기"
        usecase UC6 as "음식 사진 분석 및 영양 정보 조회하기"
        usecase UC7 as "주간·월간 성과 리포트 및 시각화 그래프 조회하기"
        
        usecase UC_Sub_Cam as "카메라 영상 데이터 수집하기"
        usecase UC_Sub_Error as "허리·무릎·어깨 정렬 오류 체크하기"
        usecase UC_Sub_Alert as "관절 각도 계산 및 경고음 출력하기"
        usecase UC_Sub_Diet as "음식 종류 인식 및 칼로리/영양소 분석하기"
    }
    
    User --> UC1
    User --> UC4
    User --> UC5
    User --> UC6
    User --> UC7
    
    UC1 ..> UC_Sub_Cam : <<include>>
    
    UC1 <.. UC2 : <<extend>>
    UC2 ..> UC_Sub_Error : <<include>>
    
    UC1 <.. UC3 : <<extend>>
    UC3 ..> UC_Sub_Alert : <<include>>
    
    UC4 <.. UC5 : <<extend>>
    
    UC7 ..> UC5 : <<include>>
    UC7 ..> UC6 : <<include>>
    UC6 ..> UC_Sub_Diet : <<include>>
