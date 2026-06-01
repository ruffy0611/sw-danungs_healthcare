# UML 다이어그램

## 유스케이스 다이어그램

```mermaid
flowchart LR
  User(["👤 일반 사용자"])
  Admin(["👤 관리자"])

  subgraph SYS ["피트니스 앱 시스템"]
    direction TB

    subgraph AUTH ["인증"]
      UC08["회원가입하기 (FR-08)"]
      UC09["로그인하기 (FR-09)"]
    end

    subgraph EXERCISE ["운동 분석 및 추천"]
      UC01["실시간 자세 분석하기 (FR-01)"]
      UC02["자세 오류 피드백 받기 (FR-02)"]
      UC03["부상 위험 경고 받기 (FR-03)"]
      UC10["피로도·목표 입력하기 (FR-10)"]
      UC04["대체 운동 추천받기 (FR-04)"]
      UC05["운동 강도 자동 조정 받기 (FR-05)"]
    end

    subgraph HEALTH ["식단 및 리포트"]
      UC06["음식 사진 분석하기 (FR-06)"]
      UC07["성과 리포트 조회하기 (FR-07)"]
    end

    subgraph FEEDBACK ["피드백"]
      UC11["기능 피드백 제출하기 (FR-11)"]
      UC12["피드백 목록 조회하기 (FR-12)"]
      UC13["피드백 검토 및 답변 등록하기 (FR-13)"]
    end

    UC01 -- "<<extend>>" --> UC02
    UC01 -- "<<extend>>" --> UC03
    UC05 -- "<<include>>" --> UC10
    UC12 -- "<<include>>" --> UC13
  end

  User --- UC08
  User --- UC09
  User --- UC01
  User --- UC04
  User --- UC05
  User --- UC06
  User --- UC07
  User --- UC11

  Admin --- UC12
  Admin --- UC13
` ``

## 클래스 다이어그램

` ``mermaid
classDiagram
  class User {
    -userId: String
    -email: String
    -password: String
    -fitnessGoal: String
    +register() : boolean
    +login() : boolean
    +inputFatigue(level: int) : void
    +submitFeedback(content: String) : void
  }

  class Admin {
    -adminId: String
    -name: String
    +reviewFeedback(feedbackId: String) : void
    +registerReply(feedbackId: String, reply: String) : void
  }

  class ExerciseSession {
    -sessionId: String
    -startTime: DateTime
    -exerciseType: String
    -fatigueLevel: int
    +start() : void
    +end() : void
    +getSummary() : SessionSummary
  }

  class PostureAnalyzer {
    -fps: int
    -jointData: List~JointAngle~
    +analyzeFrame() : PostureResult
    +detectError() : PostureError
    +detectInjuryRisk() : boolean
  }

  class PostureResult {
    -resultId: String
    -timestamp: DateTime
    -errorType: String
    -isInjuryRisk: boolean
    +sendFeedback() : void
    +triggerAlert() : void
  }

  class WorkoutRecommender {
    -userId: String
    +recommendAlternatives(muscleGroup: String) : List~Exercise~
    +adjustIntensity(fatigue: int, goal: String) : WorkoutPlan
  }

  class FoodAnalyzer {
    -analysisTimeLimit: int
    -modelVersion: String
    +analyzePhoto(image: Image) : FoodResult
    +estimateCalories() : float
    +getNutrients() : NutritionInfo
  }

  class PerformanceReport {
    -reportId: String
    -period: String
    -generatedAt: DateTime
    +generateWeekly() : Report
    +generateMonthly() : Report
    +visualizeAsGraph() : ChartData
  }

  class UserFeedback {
    -feedbackId: String
    -content: String
    -status: String
    -createdAt: DateTime
    -reply: String
    +submit() : void
    +updateStatus(status: String) : void
    +registerReply(reply: String) : void
  }

  User "1" --> "0..*" ExerciseSession : records
  User "1" --> "0..*" UserFeedback : submits
  Admin "1" --> "0..*" UserFeedback : manages
  ExerciseSession "1" *-- "1" PostureAnalyzer : uses
  PostureAnalyzer "1" --> "0..*" PostureResult : produces
  User "1" --> "1" WorkoutRecommender : uses
  WorkoutRecommender ..> ExerciseSession : depends on
  User "1" --> "1" FoodAnalyzer : uses
  User "1" --> "0..*" PerformanceReport : views
  PerformanceReport ..> ExerciseSession : aggregates
` ``
```

4. 커밋 메시지:
