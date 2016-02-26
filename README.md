# ReactJS JSX Transformer Maven Plugin
This plugin is created to simplify building ReactJS components in an Adobe Experience Manager project using Eclipse.

This is only an extended version. The original project can be viewed here: [spaulg/react-jsxtransformer-maven-plugin](https://github.com/spaulg/react-jsxtransformer-maven-plugin).
Credits to the original author, [Simon Paulger](https://github.com/spaulg).

---

### Set-up Option 1

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
```xml
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

### Set-up Option 2 (Sublime)

1. [Set-up Maven in Sublime](https://coderwall.com/p/etesrq/how-to-set-up-maven-in-sublime-text)

2. Go to Tools > Build System > New Build System

3. Copy the following into the new file
```json
{    
    "working_dir": "$file_path",	
    "shell_cmd":"mvn clean install",
    "variants": [
    	{
    		"name": "mvn clean install",
    		"shell_cmd": "mvn clean install"
    	},
    	{
    		"name": "mvn full build",
    		"shell_cmd": "mvn -P full-build clean install"
    	},
    	{ 
    		"name": "mvn clean",
    		"shell_cmd": "mvn clean"
    	},
    	{ 
    		"name": "mvn skipTests",
    		"shell_cmd": "mvn clean install -DskipTests"
    	},
    	{
    		"name": "mvn package",
    		"shell_cmd": "mvn package"
    	},
    	{
    		"name": "mvn localInstall",
    		"shell_cmd": "mvn org.apache.maven.plugins:maven-install-plugin:2.5.2:install-file -Dfile=path/to/the/jar/file -DgroupId=ph.dev.jdhrnndz -DartifactId=react-jsxtransformer-maven-plugin -Dversion=1.0-SNAPSHOT -Dpackaging=jar -DlocalRepositoryPath=path/to/the/aem/project"
    	},
    	{
    		"name": "mvn autoInstallPackage",
    		"shell_cmd": "mvn clean install -PautoInstallPackage"
    	}
    ]
}
```
4. Save as `Maven.sublime-build`

5. Prepare plugin for installation
 - Ctrl + Shift + P
 - Type *Maven Package*
 - Press Enter
 
6. Install into local repository
 - Ctrl + Shift + P
 - Type *Maven localInstall*
 - Press Enter
 
7. Add to pom.xml of the content module
```xml
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

8. Build the AEM project

**NOTES:**

-- This plugin will automatically create a folder named 'build' inside the directory provided in the configuration.

-- Delete files in the 'build' directory before building the project because the plugin will create a new 'build' folder if the existing 'build' folder already has contents.