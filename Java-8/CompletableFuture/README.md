
* ## Ch-1:
  - Intro
* ## Ch-2: 
  - *thenCombine*: For independent tasks
  - *thenCompose*: For dependent tasks
  - *thenApply vs thenCompose*
    - thenApply: When it simply returns something.
    - thenCompose: When it returns a CompletableFuture. It flattens nested CompletableFuture, unlike thenApply.
* ## Ch-3:
  - *exceptionally*: Consumes the error and has a fallback response.
  - *handle*:
    - Consumes the error and has a fallback response.
    - It can also take the result, modify it, and return.
  - *whenComplete*: To log or observe the error/result. It doesn't consume the error.
* ## Ch-4:
  - Questions
  - Comparison cheat sheet
  - What Can Be Returned in exceptionally, handle, and whenComplete
* ## Ch-5:
  - Questions - misc
* ## Ch-6:
  - Quiz
* ## Ch-7:
  - CompletableFuture Quick Summary Sheet
