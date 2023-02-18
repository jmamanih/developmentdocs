# iReport not starting after upgrading to 10.13 (high sierra) 



The failure is caused by the updating the Java version, which defaults to Java 8. To solve the issue:

1. Install Java 7.

2. Edit /Applications/Jaspersoft iReport 
Designer.app/Contents/Resources/ireport/bin/ireport
3. Add the following line before the last 'case' statement in the file: jdkhome='/Library/Java/JavaVirtualMachines/jdk1.7.***/Contents/Home'

4. Save the file.

