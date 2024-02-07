# SysON
SysON project provides an open-source web-based tooling to edit SysML v2 models. It includes a set of editors (graphical, textual, form-based, etc.) enabling users to build the various parts of system models.


## Flashcard :

![image](https://github.com/YashzAlphaGeek/SysON/assets/18661896/c8a77e71-dbe5-4c33-af37-dfb2e3bb1442)

Sirius is an open-source low-code platform to define custom web applications supporting your specific visual languages & dramatically reduces the time for creating domain-specific modeling workbenches which are integrated with SysML v2 Metamodel. Sirius Web uses PostgreSQL for its database.

The backend part of Sirius Components depends on sirius-emf-json, which is published as Maven artifacts in GitHub Packages. We need sirius-components locally, so we need GitHub Access Token so that Maven can download the sirius-emf-json artifacts.

We do have few pre-requisities to run the SysON application in your local machine. Please follow the steps keenly.

+ Java >=11
+ Docker
+ NodeJS
+ Maven >= 3.6.3
+ Enable Long Path in Windows
+ Github Personal Token (scope of read:package)
  
  <img width="592" alt="image" src="https://github.com/YashzAlphaGeek/SysON/assets/18661896/f251ffdd-fd67-4056-a882-9be0e22e967a">

You can find the Github Token in Settings -> Developer Settings (Left Corner) -> Tokens (Classic) -> Generate Token

As a next step, pre-check upon the existence of the installed libraries (Maven, Java, NodeJS) and Docker. Provide the github login details (github user id & github token).

Open the command prompt and perform the below mentioned steps one-by-one

Steps to run SysON application

+ git clone https://github.com/eclipse-syson/syson.git
+ npm login --scope=@NAMESPACE --auth-type=legacy --registry=https://npm.pkg.github.com
+ npm config set script-shell "C:\Program Files\Git\bin\bash.exe"
+ npm ci
+ npx turbo run build
+ "C:\Program Files\git\bin\bash.exe"
+ mkdir -p backend/application/syson-frontend/src/main/resources/static
+ cp -R frontend/syson/dist/* backend/application/syson-frontend/src/main/resources/static
+ exit
+ set USER={github_username}
+ set PASSWORD={token}
+ mvn -U -B -e clean verify --settings settings.xml
+ docker build -t syson backend/application/syson-application
+ cd backend/application/syson-application
+ docker-compose up
+ Run localhost:8080

## Encountered Problems & Solution :

+ Do install the above mentioned Java, Maven version and make it is been updated in the environmental variable or not.
+ We need to enable long path in windows via powershell with **administrative mode**

<pre>
  New-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Control\FileSystem" -Name "LongPathsEnabled" -Value 1 -PropertyType DWORD -Force
  git config --system core.longpaths true
</pre>

+ While building the syson application with the command (mvn -U -B -e clean verify --settings settings.xml) I came across the build failure because of the missing library

  <img width="1143" alt="image" src="https://github.com/YashzAlphaGeek/SysON/assets/18661896/12b13b92-9ed3-4726-a985-d955e4ea0e5d">

  The required maven dependency is missing the pom.xml in \syson\backend\application\syson-application-configuration.pom.xml

  <dependency>
    <groupId>commons-io</groupId>
    <artifactId>commons-io</artifactId>
    <version>2.15.1</version>
  </dependency>

  This need to be fixed from the SysON github repository by the developer. I have created a issue ticket from my side https://github.com/eclipse-syson/syson/issues/71#issue-2123795917

+ The command need to executed one after another in the command prompt.
+ The vunerabilites & warnings may exist during the installation which can be ignored.
