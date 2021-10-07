# Fault Tolerance (Resilience4j)
#### Resilience4j is a lightweight, easy-to-use fault tolerance library
#### https://resilience4j.readme.io/docs/getting-started
------
## Circuit Breaker  회로차단기
##### 특정 기간/범위 동안 api 호출 실패율, 느린호출율이 임계치를 넘으면 circuit 이 열립니다.
#### 기간/범위 설정
            slidingWindowType : COUNT_BASED
            slidingWindowSize : 100 (100 calls or 100 seconds)
            minimumNumberOfCalls : 100 calls
#### 임계치
            failureRateThreshold : 50 %
            slowCallRateThreshold : 100 %
#### 실패 기준, slow call 기준
            slowCallDurationThreshold : 60000 ms
            recordFailurePredicate : throwable -> true (모든 exception은 실패로 처리)
            ignoreException: throwable -> false (모든 exception은 무시하지 않음)
            recordExceptions : empty (실패로 처리할 Exception list)
            ignoreExceptions : empty (무시할(실패도 아니고 성공도 아님) Exception list)
#### open 상태 지속
            waitDurationInOpenState : 60000 ms
            automaticTransitionFromOpenToHalfOpenEnabled : false
#### half-open 상태 지속  (COUNT_BASED 만 지원한다고 보면 됨)
            permittedNumberOfCallsInHalfOpenState : 10  
            maxWaitDurationInHalfOpenState : 0 ms
------
## Retry 재시도
##### 어떤 조건에서 재시도를 할지, 최대 몇 번, 어떤 interval로 할지 설정

#### Retry 시도 기준
            retryOnResultPredicate : result -> false (결과값을 보고 retry 시도)
            retryExceptionPredicate : throwable -> true (Exception을 보고 retry 시도)
            retryExceptions : empty (retry할 Exception list)
            ignoreExceptions : empty (retry하지 않을 Exception list)
#### 횟수
            maxAttempts : 3
#### Retry 간 interval
            waitDuration : 500ms
            intervalFunction : numOfAttempts -> waitDuration
            intervalBiFunction : (numOfAttempts, Either<throwable, result>) -> waitDuration
#### MaxRetry 후 어떻게
            failAfterMaxRetries : false (to enable or disable throwing of MaxRetriesExceededException)
------
## Rate Limiter     요청 횟수 제한 (Client-side Rate Limiting)
##### 특정 기간동안 제한된 요청만 처리, rate limit이 걸리면 권한을 얻을 때까지 timeout 만큼 기다리다가 RequestNotPermitted 발생
        limitRefreshPeriod : 500 ns
        limitForPeriod : 50
        timeoutDuration : 5s
------
## Bulkhead.        칸막이
        waiting queue, 동시 요청 수 제한, ThreadPool 수 제한 설정, 임계치가 넘으면(maxWaitDuration이 지나거나 queueCapacity가 넘으면) BulkheadFullException이 발생
#### SemaphoreBulkhead (동시 요청 수 제한)
                maxConcurrentCalls: 25
                maxWaitDuration : 0 ms (semaphore bulkhead에 들어가기 전까지 최대 기다릴 시간)
#### FixedThreadPoolBulkhead (waitingQueue, ThreadPool 수 제한)
                coreThreadPoolSize : Runtime.getRuntime().availableProcessors()-1
                maxThreadPoolSize : Runtime.getRuntime().availableProcessors()
                queueCapacity : 100
                keepAliveDuration : 20 ms
------
## Fallback         
##### 실패시 어떻게 동작할지 설정, method 설정
------
## Reference
#### korean transition https://godekdls.github.io/Resilience4j/introduction/
#### implementation example https://reflectoring.io/bulkhead-with-resilience4j/

##### Circuit Breaker 소개/동작원리 https://yahoya.tistory.com/50
##### Circuit 상태 https://timewizhan.tistory.com/entry/Circuit-Breaker-%ED%8C%A8%ED%84%B4
##### bulkhead 예제 https://jydlove.tistory.com/74
