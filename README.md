# Maven reactor make options

Modules are named to match the Tycho integration test project
They also have the same dependency graph, expressed as Maven pom
dependencies.

```
feature2 -> feature1,bundle2
feature1 -> bundle1
```

The following builds can be run to demonstrate behaviour:


* Full build  
`mvn clean verify`  
 Expected: success


* Make feature1 with also-make  
`mvn -am -pl feature1 clean verify`  
Expected: success (parent,bundle1,feature1 built)

* Make bundle1 and bundle2 with also-make-dependents  
`mvn -amd -pl bundle1,bundle2 clean verify`  
Expected: success (bundle1,feature1,bundle2,feature2 built)

* Make feature1 and bundle2 with also-make and also-make-dependents  
`mvn -am -amd -pl feature1,bundle2 clean verify`  
Expected: success (parent,bundle1,feature1,bundle2,feature2 built)

* Make feature1 with no additional option  
`mvn -pl feature1 clean verify`  
Expected: fail (bundle1 missing)

* Make bundle1 and feature1 with also-make-dependents  
`mvn -amd -pl bundle1,feature1 clean verify`  
Expected: fail (bundle2 missing)
