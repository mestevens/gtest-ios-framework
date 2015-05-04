# gtest

## Overview

This is a framework packaged version of Google's gtest c++ library. There are three main components to this packaged version.

- gtest
 	- The actual testing framework from Google [https://code.google.com/p/googletest/](https://code.google.com/p/googletest/)
- GoogleTests.mm
	- Taken from another Matthew Stevens (not me) from [https://github.com/mattstevens/xcode-googletest](https://github.com/mattstevens/xcode-googletest) This file allows xcode to include the tests in its UI
- xcode-maven-plugin
	- The maven plugin [https://github.com/mestevens/xcode-maven-plugin](https://github.com/mestevens/xcode-maven-plugin) allows you to compile and package this project as a framework easily. Doing so also allows you to include it in another project's pom file as a dependency.
	
## Compiling

Make sure you have maven installed [https://maven.apache.org/](https://maven.apache.org/) and simply run `mvn clean install` from the directory that the pom.xml file is in. This will install this into your local maven repository under the groupId `com.google` and the artifactId `gtest` with version `1.7.0`

## Consuming the framework

After compiling, you can include this into your own project in two different ways.

### With Maven

If your main application is using maven (and the xcode-maven-plugin), you can simply include this as a dependency

```
<dependency>
	<groupId>com.google</groupId>
	<artifactId>gtest</artifactId>
	<version>1.7.0</version>
	<type>xcode-static-framewrok</type>
</dependency>
```

### Without Maven

After compiling, the framework will be found in the `target` directory underneath the root directory (for example if you clone this repository into `/Users/yourname/git/gtest-ios-framework` you could find the framework in `/Users/yourname/git/gtest-ios-framework/target`). Simply copy this framework to where you want it, and include it in your xcode project as you would normally.

## Xcode UI for tests

Once you've included the framework in your project, you still need to add the GoogleTests.mm file to your test target in order for the xcode UI to pick it up. The framework has this file included in it under `Headers/testdriver/GoogleTests.mm`. Dragging and dropping this into xcode should add it for you.

## Writing tests

After this is all set-up you can create a cpp file with gtest test cases. The only requirement at this point is that you make sure it's included in your `Compile Sources` build phase in your test bundle.