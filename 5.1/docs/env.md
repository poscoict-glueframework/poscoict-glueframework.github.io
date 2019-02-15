# 사전준비

이번 장의 내용을 응용해서 프로젝트에 맞는 개발 환경 구성할 수 있습니다.  
윈도우 환경이라고 가정하며, 다음과 같은 툴을 사용한다고 가정합니다. 

* Java 8
* Maven 
* git
* Eclipse ( 또는 Spring Tool Suite )

주요 디렉토리 구조는 다음과 같다고 가정합니다.  

> /infra/jdk1.8.0_192  
> /infra/apache-maven-3.5.4  
> /infra/GlueSDK  
> /ide/eclipse  
> /workspace  

## <a name="java"></a>Java 설치

Java SE 8을 설치합니다. 

1. 다운로드  

    * [https://www.oracle.com/technetwork/java/javase/downloads/index.html](https://www.oracle.com/technetwork/java/javase/downloads/index.html)

    License Agreement 를 체크하고 파일을 다운로드 합니다.

2. 설치  

    * *`C:\infra\jdk1.8.0_192`* 에 설치되었다고 가정합니다.  
    java, keytool, cacerts 등의 위치는 다음과 같습니다. 

        ```
        C:\infra\jdk1.8.0_192\bin\java.exe
        C:\infra\jdk1.8.0_192\bin\keytool.exe
        C:\infra\jdk1.8.0_192\jre\lib\security\cacerts
        ```

3. 확인 ( 명령 프롬프트에서 실행 ) 

    ```
    > C:\infra\jdk1.8.0_192\bin\java -version
    ```
    환경 변수 ( *`path=%path%;C:\infra\jdk1.8.0_192\bin`* ) 에 Java 를 추가하면, 다음과 같이 확인가능합니다.

    ```
    > java -version
    ```

## <a name="git"></a>Git 설치

예제 소스는 git을 통해 공유하며, 커맨드 실행 환경은 Git Bash로 가정합니다.  

1. git 다운로드  

    * [https://git-scm.com/downloads](https://git-scm.com/downloads)

    Latest source Release 버전으로 다운로드 합니다. 

2. 설치

3. Git Bash 실행  ( 윈도우 시작 > 모든 프로그램 > Git > Git Bash )

4. 버전 확인  ( Git Bash 에서 실행 ) 

    ```bash
    $ git --version
    ```

5. 예제 가져오기 ( Git Bash 에서 실행 )  

    ```bash
    $ cd /c/workspace
    $ git clone https://github.com/poscoict-glueframework/glue-examples.git
    $ ls /c/workspace/glue-examples -l
    ```

## <a name="maven"></a>Maven 설치

Maven을 설치합니다. Maven 커맨드를 직접 사용하기위해 설치합니다.  
Local Repository(.m2)에 glue library, arche-type 등을 3rd party jar로서 설치하기 위해 필요합니다.

1. maven 다운로드

    * [http://maven.apache.org/download.cgi](http://maven.apache.org/download.cgi)  
    
    Binary zip archive 로 다운로드 합니다. 

2. 설치(압축풀기)

    * *`C:\infra\apache-maven-3.5.4`* 에 설치했다고 가정합니다.  
    mvn, settings 등의 위치는 다음과 같습니다. 

        ```
        C:\infra\apache-maven-3.5.4\bin\mvn
        C:\infra\apache-maven-3.5.4\bin\mvn.cmd
        C:\infra\apache-maven-3.5.4\conf\settings.xml
        ```

3. 실행파일 수정하기

    * *C:\infra\apache-maven-3.5.4\bin\mvn* 파일을 수정한다.  
    * *C:\infra\apache-maven-3.5.4\bin\mvn.cmd* 파일을 수정한다.  
    mvn과 mvn.cmd 파일에  맨 위에 JAVA_HOME 을 설정합니다. 

        ```
        @echo off
        set JAVA_HOME=C:\infra\jdk1.8.0_192
        @REM Licensed to the Apache Software Foundation (ASF) under one
        @REM or more contributor license agreements.  See the NOTICE file
        @REM distributed with this work for additional information
        @REM regarding copyright ownership.  The ASF licenses this file
        @REM to you under the Apache License, Version 2.0 (the
        @REM "License"); you may not use this file except in compliance
        @REM with the License.  You may obtain a copy of the License at
        ```

        ```
        JAVA_HOME=C:/infra/jdk1.8.0_192
        #!/bin/sh
        
        # Licensed to the Apache Software Foundation (ASF) under one
        # or more contributor license agreements.  See the NOTICE file
        # distributed with this work for additional information
        # regarding copyright ownership.  The ASF licenses this file
        # to you under the Apache License, Version 2.0 (the
        # "License"); you may not use this file except in compliance
        # with the License.  You may obtain a copy of the License at
        ```

4. 버전확인 ( Git Bash에서 실행)

    ```bash
    $ /c/infra/apache-maven-3.5.4/bin/mvn -version
    ```
    환경 변수 ( *`path=%path%;C:\infra\apache-maven-3.5.4\bin`* ) 에 Maven을 추가하면, 다음과 같이 확인가능합니다. 

    ```bash
    $ mvn -version
    ```

5. 예제 빌드하기 ( Git Bash에서 실행 ) 

    ```
    $ cd /c/workspace/glue-examples/quick-start
    $ /c/infra/apache-maven-3.5.4/bin/mvn  package
    $ /c/infra/jdk1.8.0_192/bin/java  -jar  target/demo.jar
    ```

## <a name="eclipse"></a>Eclipse 설치

IDE는 Eclpse를 기본으로 합니다.  
Eclipse 는 다양한 Package 를 제공하나, 다음 2가지 중 하나를 다운로드합니다.

* Eclipse IDE for Java Developers
* Eclipse IDE for Java EE Developers

다른 IDE(Spring Tool Suite, IntelliJ등) 도 있으나, Glue Plugin은 Eclipse 용만 제공됩니다.  

1. eclipse 다운로드

    * [https://www.eclipse.org/downloads/packages/](https://www.eclipse.org/downloads/packages/)
    
    Eclipse IDE for Java Developers 또는 Eclipse IDE for Java EE Developers 패키지로 다운로드 합니다. 

2. 설치(압축풀기)

    * *`C:\ide\eclipse`* 에 설치했다고 가정합니다.  
    eclipse, ini 파일 등의 위치는 다음과 같습니다. 

        ```
        C:\ide\eclipse\eclipse.exe  # 실행파일
        C:\ide\eclipse\eclipse.ini  # ini파일
        C:\ide\eclipse\dropins      # GluePlugin위치
        ```

3. 환경파일 수정하기

    * *C:\ide\eclipse\eclipse.ini* 파일을 수정한다.  
    eclipse.ini 파일에서 _-vmargs_ 를 찾아서 그 위에 다음을 추가한다.  

        ```
        -vm
        C:/infra/jdk1.8.0_192/bin/javaw.exe
        ```

    *eclipse.ini* 의 내용은 다음과 같습니다. 

    ```
    -startup
    plugins/org.eclipse.equinox.launcher_1.5.100.v20180827-1352.jar
    --launcher.library
    plugins/org.eclipse.equinox.launcher.win32.win32.x86_64_1.1.800.v20180827-1352
    -product
    org.eclipse.epp.package.java.product
    -showsplash
    org.eclipse.epp.package.common
    --launcher.defaultAction
    openFile
    --launcher.defaultAction
    openFile
    --launcher.appendVmargs
    -vmargs
    .. 중략 ..
    ```

4. eclipse 실행하기  
workspace는 *`C:\workspace`* 로 지정한다고 가정합니다. 

    메뉴 > Window > Preference > General > Workspace   
    Text file encoding 을 UTF-8 로 했다고 가정합니다. 

5. 바로가기 만들기  

    * workspace 를 여러개 사용할 경우 `-data` 옵션을 이용해서 eclipse를 여러 개 실행할 수 있습니다.  

        ```
        C:\ide\eclipse\eclipse.exe -data C:\workspace
        ```

    * plugin 변경 사항이 반영되지 않을 경우 `-clean` 옵션을 추가할 수 있습니다. 
 
        ```
        C:\ide\eclipse\eclipse.exe -clean -data C:\workspace
        ```

## Ref. 참고

* [Java Documentation](https://docs.oracle.com/en/java/)
* [Git Documentation](https://git-scm.com/docs)
* [Maven User Centre](http://maven.apache.org/users/index.html)
* [Eclipse](https://www.eclipse.org)
* [Spring Tools 4](https://spring.io/tools)
* [IntelliJ IDEA](https://www.jetbrains.com/idea/)