# Lft4Se
This project assumes you have followed the LeanFT set up instructions found on https://leanft-help.saas.hpe.com/en/14.01/HelpCenter/Content/HowTo/Sel_LeanFT4SelT.htm


For adding to a local .m2 cache when these jars are not on your internal maven repo, I use the following lines either from a command line or from with in the terminal window (in my case the IntelliJ Terminal window)

### Windows
mvn install:install-file -Dfile="C:\Program Files (x86)\HP\Unified Functional Testing\Selenium SDK\Java\com.hpe.lft.selenium.jar" -DgroupId=com.hpe.lft -DartifactId=selenium-sdk -Dversion=14.1.0 -Dpackaging=jar

mvn install:install-file -Dfile="C:\Program Files (x86)\HP\Unified Functional Testing\Selenium SDK\Java\com.hpe.lft.selenium-javadoc.jar" -DgroupId=com.hpe.lft -DartifactId=selenium-sdk -Dversion=14.1.0 -Dpackaging=jar -Dclassifier=Javadoc

### Unix
mvn install:install-file -Dfile="/opt/leanft/selenium-sdk/Java/com.hpe.lft.selenium.jar" -DgroupId=com.hpe.lft -DartifactId=selenium-sdk -Dversion=14.1.0 -Dpackaging=jar

mvn install:install-file -Dfile="/opt/leanft/selenium-sdk/Java/com.hpe.lft.selenium-javadoc.jar" -DgroupId=com.hpe.lft -DartifactId=selenium-sdk -Dversion=14.1.0 -Dpackaging=jar -Dclassifier=Javadoc

And you should already see this in your pom.xml if you created the project from the templates

```
<dependency>
     <groupId>org.seleniumhq.selenium</groupId>
     <artifactId>selenium-java</artifactId>
     <version>2.53.1</version>
<dependency>


<dependency>
     <groupId>com.hpe.lft</groupId>
     <artifactId>selenium-sdk</artifactId>
     <version>14.1.0</version>
<dependency>
```
The script has been modified to make use of the released version of the com.hpe.lft.selenium-sdk file

```
<dependency>
     <groupId>com.hpe.lft</groupId>
     <artifactId>selenium-sdk</artifactId>
     <version>RELEASE</version>
<dependency>
```

### getDrivers.sh
The getDrivers.sh is a small utility to aid in getting the selenium driver required for this script.  This script was created to use the Selenium Chrome driver and as of the time of this writing, the driver 2.27 was the last driver version tested to work.

The script assumes your chromedriver is in the /opt/selenium/<VER> folder.  If you will be placing it in a folder other than that, then you will need to edit the test.

To use the getDriver.sh, create the directory /opt/selenium and copy getDriver.sh to the folder and then run:

```
./getDrivers.sh 2.27
```

If you are using the IntelliJ container to run this test, you will need to perform the above steps inside the IntelliJ container.

#### Note for execution from command line
java -cp .;junit-4.12.jar;presales-1.0-SNAPSHOT.jar;hamcrest-core-1.3.jar;selenium-server-standalone-2.53.1.jar;com.hpe.lft.selenium.jar org.junit.runner.JUnitCore SeleniumTest

The above assumes:
- you have done a maven deploy goal
- all the relavant *.jar files are in the same directory
- to get junit.jar and hamcrest-core.jar if not on your system already https://github.com/junit-team/junit4/wiki/Download-and-Install

