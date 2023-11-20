# Grails 6 Bugs 

## Compiled views outside of grails-app folder not included in views.properties

https://github.com/grails/grails-gradle-plugin/issues/257

Previously worked prior to Grails 6.1.0

Demo
```
git clone https://github.com/codeconsole/grails6bugs
cd grails6bugs
./gradlew clean bootJar
# notice src/main/webapp/test/hello.gsp was correctly compiled
unzip -l build/libs/grails6bugs-0.1.jar|grep index_gsp
unzip -p build/libs/grails6bugs-0.1.jar BOOT-INF/classes/gsp/views.properties
```

Notice `/test/hello.gsp` gsp in views.properties
```
#Precompiled views for grails6bugs
#Mon Nov 20 10:23:18 CST 2023
/WEB-INF/grails-app/views/error.gsp=gsp_grails6bugserror_gsp
/WEB-INF/grails-app/views/index.gsp=gsp_grails6bugsindex_gsp
/WEB-INF/grails-app/views/layouts/main.gsp=gsp_grails6bugs_layoutsmain_gsp
/WEB-INF/grails-app/views/notFound.gsp=gsp_grails6bugsnotFound_gsp
```

Now verify it worked in Grails 6.0.0
```
git checkout 6.0.0
./gradlew clean bootJar
unzip -p build/libs/grails6bugs-0.1.jar BOOT-INF/classes/gsp/views.properties
```

Notice `/test/hello.gsp` is now listed 
```
#Precompiled views for grails6bugs
#Mon Nov 20 10:24:09 CST 2023
/WEB-INF/grails-app/views/error.gsp=gsp_grails6bugserror_gsp
/WEB-INF/grails-app/views/index.gsp=gsp_grails6bugsindex_gsp
/WEB-INF/grails-app/views/layouts/main.gsp=gsp_grails6bugs_layoutsmain_gsp
/test/hello.gsp=gsp_grails6bugs_testhello_gsp
/WEB-INF/grails-app/views/notFound.gsp=gsp_grails6bugsnotFound_gsp
```

http://localhost:8080/test/hello.gsp



