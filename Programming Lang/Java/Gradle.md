
`gradle init`
to initailze the project

```bash
$ gradle init

Select type of project to generate:
  1: basic
  2: application
  3: library
  4: Gradle plugin
Enter selection (default: basic) [1..4] 2

Split functionality across multiple subprojects?:
   1: no - only one application project
   2: yes - application and library projects
Enter selection (default: no - only one application project) [1..2] 2

Select implementation language:
  1: C++
  2: Groovy
  3: Java
  4: Kotlin
  5: Scala
  6: Swift
Enter selection (default: Java) [1..6] 3

Select build script DSL:
  1: Groovy
  2: Kotlin
Enter selection (default: Groovy) [1..2] 1

Select test framework:
  1: JUnit 4
  2: TestNG
  3: Spock
  4: JUnit Jupiter
Enter selection (default: JUnit 4) [1..4]

Project name (default: demo):
Source package (default: demo):


BUILD SUCCESSFUL
2 actionable tasks: 2 executed
```


folder meaning:
* `gradle/` folder for wrapper files
* `gradlew` & `gradlew.bat` gradle wrapper start script
* `settings.gradle` settings to define build name and subprojects
* `build.gradle` configure dependency of the build logic
* `buildSrc/src/main/groovy` source folder for convention plugins written in Groovy


## Settings.gradle

```groovy
rootProject.name = 'demo'
include('app', 'list', 'utilities')
```

* `rootProject.name`
* `include` : including subproject

## Convention plugins

this plugins is for sharing same build logic and configuration file between multiple sub project.

we define our shared configuration in
`buildSrc/src/main/groovy/demo.java-common-conventions.gradle`
```groovy
plugins {
    id 'java' 
}

repositories {
    mavenCentral() 
}

dependencies {
    constraints {
        implementation 'org.apache.commons:commons-text:1.9' 
    }

    testImplementation 'org.junit.jupiter:junit-jupiter:5.9.1' 
}

tasks.named('test') {
    useJUnitPlatform() 
}
```

* `repositories` for source for external dependencies


`buildSrc/src/main/groovy/demo.java-library-conventions.gradle`
```groovy
plugins {
    id 'demo.java-common-conventions' 

    id 'java-library' 
}
```

`buildSrc/src/main/groovy/demo.java-application-conventions.gradle`
```groovy
plugins {
    id 'demo.java-common-conventions' 

    id 'application' 
}
```

these 2 comventions apply the basic `demo.java-common-conventions`
