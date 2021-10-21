# Jenkins Pipeline
##### official site: https://www.jenkins.io/doc/book/pipeline/

### What is Jenkins Pipeline
##### CI delivery파이프라인을 Jenkins에 구현하고 통합하는 것을 지원하는 플러그인 모음

<img src="https://www.jenkins.io/doc/book/resources/pipeline/realworld-pipeline-flow.png" width="800px" title="Example CD Pipeline"/>

### Why Pipeline?
##### Code : 코드로 구현되며 일반적으로 소스 제어에 체크인되어 팀이 전달 파이프라인을 편집, 검토 및 반복할 수 있다.
##### Durable : can survive both planned and unplanned restarts of the Jenkins controller.
##### Pausable : can optionally stop and wait for human input or approval before continuing the Pipeline run
##### Versatile : 분기/조인, 루프 및 병렬 작업 수행 기능을 포함하여 복잡한 실제 CD 요구 사항을 지원한다.
##### Extensible : supports custom extensions to its DSL [1] and multiple options for integration with other plugins.

### Pipeline basic concepts
##### Pipeline
##### Agent
##### Node
##### Stage
##### Step

### Example 
##### Declarative Pipeline
```
pipeline {
    agent any 
    stages {
        stage('Build') { 
            steps {
                // 
            }
        }
        stage('Test') { 
            steps {
                // 
            }
        }
        stage('Deploy') { 
            steps {
                // 
            }
        }
    }
}
```
##### Scripted Pipeline
```
node {  
    stage('Build') { 
        // 
    }
    stage('Test') { 
        // 
    }
    stage('Deploy') { 
        // 
    }
}
```
### Pipeline Syntax
##### Agent 
###### Parameter: any, none, label, node, docker, dockerfile, kubernetes
###### Common Options: label, customWorkspace, reuseNode, 
##### post
###### Condition: always, changed, fixed, regression, aborted, failure, success, unstable, unsuccessful, cleanup
##### stages
###### steps
##### environment
###### Secret, Username and password, SSH with Private Key
##### options
###### buildDiscarder, checkoutToSubdirectory, disableConcurrentBuilds, disableResume, newContainerPerStage, overrideIndexTriggers
###### preserveStashes, quietPeriod, retry, skipDefaultCheckout, skipStagesAfterUnstable, timeout

##### parameters
###### string, text, booleanParam, choice, password
##### triggers 
###### cron, pollSCM, upstream

##### tools
###### maven, jdk, gradle
