# ReactJS JSX Transformer Maven Plugin
This plugin is created to simplify building ReactJS components in an Adobe Experience Manager project using Eclipse.

This is only an extended version. The original project can be viewed here: [spaulg/react-jsxtransformer-maven-plugin](https://github.com/spaulg/react-jsxtransformer-maven-plugin).
Credits to the original author, [Simon Paulger](https://github.com/spaulg).

---

### Set-up

1. Prepare plugin for installation
-- run `mvn package` inside the project directory then look for the path of the jar created and save it for later.

2. Install into local repository
```shell
mvn org.apache.maven.plugins:maven-install-plugin:2.5.2:install-file
    -Dfile=path/to/the/jar/file
    -DgroupId=ph.dev.jdhrnndz
    -DartifactId=react-jsxtransformer-maven-plugin
    -Dversion=1.0-SNAPSHOT
    -Dpackaging=jar
    -DlocalRepositoryPath=path/to/the/aem/project
```

3. Add to pom.xml of the content module
```
<plugin>
    <groupId> ph.dev.jdhrnndz </groupId>
    <artifactId> react-jsxtransformer-maven-plugin </artifactId>
    <version> 1.0-SNAPSHOT </version>

    <executions>
        <execution>
            <goals>
                <goal>transform</goal>
            </goals>
        </execution>
    </executions>
    <configuration>
        <sourcePathArray>
            <param>${basedir}/path/containing/jsx/1</param>
            <param>${basedir}/path/containing/jsx/2</param>
        </sourcePathArray>
    </configuration>
</plugin>
```
4. Build the AEM project
```shell
mvn clean install -PautoInstallPackage
```

**NOTES:**

-- This plugin will automatically create a folder named 'build' inside the directory provided in the configuration.

-- Delete files in the 'build' directory before building the project because the plugin will create a new 'build' folder if the existing 'build' folder already has contents.