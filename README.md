# Milestone 4
## 1. Open Project
- Open project in Intellij
- Choose Maven to build the project
## 2. Run
### Open test file
- Locate file at `src/test/java/org/json/junit/JSONObjectTest.java`
- Search for methods `jsonObjectToStreamTest`
### Run test
- Click run button next to method signature

## 3. Notes
- Use recursive DFS to traverse all the key-value pair in the JSONObject in pre-order
- Process JSONArray and nested JSONArray
- Use `Stream.concat()` to make an object streamable
- In the output of test method `jsonObjectToStreamTest`, the result can be compared


# Milestone 3
## 1. Open Project
- Open project in Intellij
- Choose Maven to build the project
## 2. Run
### Open test file
- Locate file at `src/test/java/org/json/junit/XMLTest.java`
- Search for methods `testToJSONObjectWithKeyTransformer`
### Run test
- Click run button next to method signature
## 3. Notes

### `parse`

Wrap the parse method with fewer arguments for keyTransformer.
```java
    private static boolean parse(XMLTokener x, JSONObject context, String name, XMLParserConfiguration config,
                                 Function<String, String> keyTransformer) {
        return parse(x, context, name, config, null, 0, null, false, keyTransformer, true);
    }
```

### `keyTransformer`
**6-line logic for this milestone**

In the implementation, the **keyTransformer** logic allows key change during parse. Therefore, one traversal is enough, which provides a better performance. In addition, the code utilize the existing variable to save the changed name, which saves space cost.

Apply `keyTransformer` method to `tagName` to change the key.
```java
            // key transform
            if(isTransform) {
                tagName = keyTransformer.apply(tagName);
            }
```
And apply the method to token at `else if (token == SLASH) ` block for close tag match.
```java
            // check if doing transforming, make a matching key
            if(isTransform) {
                token = keyTransformer.apply(token.toString());
            }
```
---
# Milestone 2
## 1. Open Project
- Open project in Intellij
- Choose Maven to build the project
## 2. Run
### Open test file
- Locate file at `src/test/java/org/json/junit/XMLTest.java`
- Search for methods `testToJSONObjectWithPath`. It takes in charge of task 1
- Search for methods `testToJSONObjectWithPathWithReplacement`. It's in charge of task2
### Run test
- Click run button next to method signature

## 3. Notes
notes that help to understand code

1. To make best use of existing code, added logic is added to `parse` method;
2. To keep the existing code untouched, `parse` method is overridden into 3 methods with different parameters;
3. Use `skipPast` method to run faster;
4. Unable to process JSONArray

---

![Json-Java logo](https://github.com/stleary/JSON-java/blob/master/images/JsonJava.png?raw=true)

<sub><sup>image credit: Ismael P??rez Ortiz</sup></sub>


JSON in Java [package org.json]
===============================

[![Maven Central](https://img.shields.io/maven-central/v/org.json/json.svg)](https://mvnrepository.com/artifact/org.json/json)

**[Click here if you just want the latest release jar file.](https://search.maven.org/remotecontent?filepath=org/json/json/20211205/json-20211205.jar)**


# Overview

[JSON](http://www.JSON.org/) is a light-weight language-independent data interchange format.

The JSON-Java package is a reference implementation that demonstrates how to parse JSON documents into Java objects and how to generate new JSON documents from the Java classes.

Project goals include:
* Reliable and consistent results
* Adherence to the JSON specification 
* Easy to build, use, and include in other projects
* No external dependencies
* Fast execution and low memory footprint
* Maintain backward compatibility
* Designed and tested to use on Java versions 1.6 - 1.11

The files in this package implement JSON encoders and decoders. The package can also convert between JSON and XML, HTTP headers, Cookies, and CDL.

The license includes this restriction: ["The software shall be used for good, not evil."](https://en.wikipedia.org/wiki/Douglas_Crockford#%22Good,_not_Evil%22) If your conscience cannot live with that, then choose a different package.

# If you would like to contribute to this project

For more information on contributions, please see [CONTRIBUTING.md](https://github.com/stleary/JSON-java/blob/master/docs/CONTRIBUTING.md)

Bug fixes, code improvements, and unit test coverage changes are welcome! Because this project is currently in the maintenance phase, the kinds of changes that can be accepted are limited. For more information, please read the [FAQ](https://github.com/stleary/JSON-java/wiki/FAQ).

# Build Instructions

The org.json package can be built from the command line, Maven, and Gradle. The unit tests can be executed from Maven, Gradle, or individually in an IDE e.g. Eclipse.
 
**Building from the command line**

*Build the class files from the package root directory src/main/java*
````
javac org/json/*.java
````

*Create the jar file in the current directory*
````
jar cf json-java.jar org/json/*.class
````

*Compile a program that uses the jar (see example code below)*
````
javac -cp .;json-java.jar Test.java (Windows)
javac -cp .:json-java.jar Test.java (Unix Systems)
````

*Test file contents*

````
import org.json.JSONObject;
public class Test {
    public static void main(String args[]){
       JSONObject jo = new JSONObject("{ \"abc\" : \"def\" }");
       System.out.println(jo.toString());
    }
}
````

*Execute the Test file*
```` 
java -cp .;json-java.jar Test (Windows)
java -cp .:json-java.jar Test (Unix Systems)
````

*Expected output*

````
{"abc":"def"}
````

 
**Tools to build the package and execute the unit tests**

Execute the test suite with Maven:
```
mvn clean test
```

Execute the test suite with Gradlew:

```
gradlew clean build test
```

# Notes

For more information, please see [NOTES.md](https://github.com/stleary/JSON-java/blob/master/docs/NOTES.md)

# Files

For more information on files, please see [FILES.md](https://github.com/stleary/JSON-java/blob/master/docs/FILES.md)

# Release history:

For the release history, please see [RELEASES.md](https://github.com/stleary/JSON-java/blob/master/docs/RELEASES.md)
