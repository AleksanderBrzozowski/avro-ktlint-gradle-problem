This project demonstrates the problem when avro gradle plugin is used alongside ktlint.

When you run:
```shell
./gradlew clean build
```

You will see fallowing log message:
```
Task :runKtlintCheckOverMainSourceSet
Execution optimizations have been disabled for task ':runKtlintCheckOverMainSourceSet' to ensure correctness due to the following reasons:
  - Gradle detected a problem with the following location: '/Users/aleksander.brzozowsk/IdeaProjects/education/avro-ktlint-gradle/build/generated-main-avro-java'. Reason: Task ':runKtlintCheckOverMainSourceSet' uses this output of task ':generateAvroJava' without declaring an explicit or implicit dependency. This can lead to incorrect results being produced, depending on what order the tasks are executed. Please refer to https://docs.gradle.org/7.4.1/userguide/validation_problems.html#implicit_dependency for more details about this problem.
```

The problem can be fixed with following code added to `build.gradle`:
```groovy
tasks.named("runKtlintCheckOverMainSourceSet").configure { dependsOn(":generateAvroJava") }
```
