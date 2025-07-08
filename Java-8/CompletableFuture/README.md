
* ## Ch-1:
  - Intro
* ## Ch-2: 
  - *thenCombine*: For independent tasks
  - *thenCompose*: For dependent tasks
  - *thenApply vs thenCompose*
    - thenApply: When it simply returns something.
    - thenCompose: When it returns a CompletableFuture. It flattens nested CompletableFuture unlike thenApply.
