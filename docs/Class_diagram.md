## 클래스 다이어그램

```mermaid
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
```
