# geb-spock-reports

 [ ![Download](https://api.bintray.com/packages/aoepeople/libraries/geb-spock-reports/images/download.svg) ](https://bintray.com/aoepeople/libraries/geb-spock-reports/_latestVersion)

geb-spock-reports is a library to integrate [Geb](http://gebish.org/) screenshots into [spock-reports](https://github.com/renatoathaydes/spock-reports).
  
## Usage

Add `jcenter()` to the repositories in your  `build.gradle`.

```groovy
repositories {
    jcenter()
}
``` 

Add dependencies.

```groovy
dependencies {
    testCompile 'com.aoe:geb-spock-reports:0.2.0'
    
    // required spock libraries
    testCompile "org.spockframework:spock-core:1.1-groovy-2.4-rc-4"
    testCompile ("com.athaydes:spock-reports:1.6.0") { transitive = false }
    
    // required geb libraries
    testCompile "org.gebish:geb-spock:2.2"
    
    // you may also need selenium support
    testCompile "org.seleniumhq.selenium:selenium-firefox-driver:3.9.1"
    testCompile "org.seleniumhq.selenium:selenium-support:3.9.1"
    
    // recommended for logging
    testCompile 'org.slf4j:slf4j-api:1.7.13'
    testCompile 'org.slf4j:slf4j-simple:1.7.13'
}
```

#### Configure Geb

Create a `GebConfig.groovy` in `src/test/resources`.
See [Book of Geb](http://gebish.org/manual/current/#configuration) for further configuration.

```groovy
import com.aoe.gebspockreports.GebReportingListener

reportingListener = new GebReportingListener()
reportsDir = 'build/geb-spock-reports'
```

#### Configure spock-reports

Create a properties file named 

`src/test/resources/META-INF/services/com.athaydes.spockframework.report.IReportCreator.properties`


The following properties are required.

```properties
# output directory relative to working directory
com.athaydes.spockframework.report.outputDir=build/geb-spock-reports

# let's use the TemplateReportCreator to utilize our custom template
com.athaydes.spockframework.report.IReportCreator=com.athaydes.spockframework.report.template.TemplateReportCreator

# if true, code blocks are shown
com.athaydes.spockframework.report.showCodeBlocks=true

# specific properties to the TemplateReportCreator
com.athaydes.spockframework.report.template.TemplateReportCreator.specTemplateFile=/templates/spec-template.html
com.athaydes.spockframework.report.template.TemplateReportCreator.reportFileExtension=html
com.athaydes.spockframework.report.template.TemplateReportCreator.summaryTemplateFile=/templates/summary-template.html
com.athaydes.spockframework.report.template.TemplateReportCreator.summaryFileName=index.html
```

See the [spock-reports documentation](https://github.com/renatoathaydes/spock-reports#customizing-the-reports) for further configuration.

---

**Important:** Make sure that the `reportDir` in `GebConfig.groovy` matches the `outputDir` in the `.properties` file!

#### Configure geb-spock-reports

You can configure if pagination should be enabled the summary page.
If pagination is disabled, *all* specifications results will be shown in the table.

By default, pagination is disabled and this config file is not needed.
To overwrite it, create a `GebSpockReportsConfig.groovy` file in `src/test/resources/` with the following content:

```groovy
// configure pagination on summary template
pagination {
    enabled = true
    pageSize = 20
}
```

## License

This project is licensed under the [Apache Software License, Version 2.0](http://www.apache.org/licenses/LICENSE-2.0).

See [`LICENSE`](LICENSE) for more information.

    Copyright 2017-2018 Tilman Ginzel, AOE GmbH

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

        http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.