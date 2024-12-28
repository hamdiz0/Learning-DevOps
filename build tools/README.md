# `BUILD TOOLS`

- [Artifacts](#artifacts-)
- [Settings up build tools](#settings-up-build-tools-)
    - [Linux](#linux-)
    - [Win](#win-)
- [Basic commands](#basic-commands-)
    - [Maven & Gradle](#maven--gradle-)
    - [Npm](#npm-)
- [Dependencies and plugins](#dependencys-and-plugins-)
- [Npm/Yarn vs Gradle/Maven (package managers)](#npmyarn-vs-gradlemaven-package-managers-)


# `artifacts` :

    * apps need to be deployed on a production server 
    * application code and its dependencies must be packaged into a single movable file called an artifcat wich's esier to deploy on servers 
    * building the code / packaging :
        - compile the code
        - compress into a single file
    * the artifact can be deployed on multiple servers like development ,test and production so there should be a back up in case of failure ,so artifacts must be stored on an artifact repository like nexus
    * an artifact can have a specific format/extention depending on the programming lanuage used :
        - java => .jar or .war 
        - python => .pyz or .whl
        - nodejs => .zip or .tar

# `settings up build tools` :

## `linux` :

    * java :
		- apt install openjdk-<version> (17)-jdk
	* SDK to install gradle :
		- curl -s "https://get.sdkman.io" | bash
		- source "$HOME/.sdkman/bin/sdkman-init.sh"
		- sdk install gradle <version> (7.4)
    * maven :
        - apt install maven
    * nodejs && npm :
        - apt install nodejs npm

## `win` :

    * downlowd java <version> ,maven and gradle 
    * edit the system environment variables => environmeent variables under advanced tab 
    * add java ,maven and gradle paths inside the "path" variable (double click)
    * add "JAVA_HOME" along with th "path" variable in the system variable section
    * for nodejs & npm download the installer from official website 

# `basic commands` :

## `maven & gradle` :
    * run a jar file :
        - java -jar <file.jar>
    * maven :
        - mvn archetype:generate \
        > -DgroupId=com.example -DartifactId=<name> \ 
        > -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
        - mvn clean install|package (in the project folder to build it)
        * basic structure :  
            my-app
            ├── pom.xml
            └── src
                ├── main
                │   └── java
                │       └── com
                │           └── example
                │               └── App.java
                └── test
                    └── java
                        └── com
                            └── example
                                └── AppTest.java
    * gradle :
        - gradle init
        - gradle build
        * basic structure :
            my-app
            ├── build.gradle
            ├── settings.gradle
            └── src
                ├── main
                │   └── java
                │       └── com
                │           └── example
                │               └── App.java
                └── test
                    └── java
                        └── com
                            └── example
                                └── AppTest.java
    * pip :
    - python -m venv <name> (best-practice to create a virtual environment)
    - pip install setuptools wheel
    - python setup.py sdist bdist_wheel (this will create tar files under dist/)
    * basic structure :
            my_project/
            ├── my_project/
            │   ├── __init__.py       # Makes this a package
            │   ├── module1.py        # Your module(s)
            │   ├── module2.py
            ├── tests/
            │   └── test_module1.py   # Optional test suite
            ├── setup.py              # Metadata and package configuration
            ├── README.md             # Optional: Project description
            ├── LICENSE               # Optional: License file
            ├── requirements.txt      # Optional: List of dependencies
            └── MANIFEST.in           # Optional: Include additional files in the package
        


# `dependencys and plugins` :

    * for maven you can manage dependencies and plugins in the "pom.xml" file :
        <plugins>
            <plugin>
				<groupId>org.apche.maven.plugins</groupId>
				<artifactId>maven-deploy-plugin</artifactId>
				<version>3.1.1</version>
			</plugin>
        </plugins>

        <dependencies>
            <dependency>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-starter-web</artifactId>
                <version>3.0.5</version>
            </dependency>
        </dependencies>
    * for gradle it's found in build.gradle :
        plugins {
            id 'java'
            id 'org.springframework.boot' version '3.1.0'
            id 'io.spring.dependency-management' version '1.1.0'
            id 'maven-publish'
        }
        dependencies {
            implementation 'org.springframework.boot:spring-boot-starter-web'
            implementation group: 'net.logstash.logback', name: 'logstash-logback-encoder', version: '5.2'
            implementation 'javax.annotation:javax.annotation-api:1.3.2'
            testImplementation group: 'junit', name: 'junit', version: '4.12'
        }
    * for npm it's in package.json :
        "dependencies": {
            "express": "^4.19.2",
            "http-proxy-middleware": "^1.0.4",
            "react-nodejs-example": "file:"
        },      
    * for pip a file "setup.py" must be created :
        from setuptools import setup, find_packages
        setup(
            name="my_project",              # Your package name
            version="0.1",                  # Package version
            description="A description of my project",  # Short description
            author="Your Name",             # Your name
            author_email="your_email@example.com",  # Your contact email
            url="https://github.com/yourrepo/my_project",  # Project URL (optional)
            packages=find_packages(),       # Automatically find packages in your project
            install_requires=[              # Optional: list your dependencies
                "numpy",
                "requests",
            ],
            entry_points={                  # Optional: Entry points for command-line scripts
                'console_scripts': [
                    'my_project=my_project.module1:main_function',  # Custom command
                ],
            },
            classifiers=[                   # Optional: Metadata classifiers
                "Programming Language :: Python :: 3",
                "License :: OSI Approved :: MIT License",
                "Operating System :: OS Independent",
            ],
            python_requires='>=3.6',        # Specify Python version compatibility
        )
        



## `npm` :
    
    * start basic project :
        - npm init -y 
    * you can start with popular templates :
        - npx create-react-app my-app
    * install needed dependencies :
        - npm install (installs dependencies found in the package.json)
        - npm install <dependencie> --save (install a dependencie and add it to the package.jso file)
    * run ,build & test :
        - npm run start
        - npm run test
        - npm run build
    * package the application :
        - npm pack (file.tgz "tar")
    * basic structure :
        my-app
        ├── package.json
        ├── index.js
        └── test
            └── test.js

# `npm/yarn vs gradle/maven (package managers)` :

    * unlike the java artifacts ,node artifacts does not contain the application dependencies but there is way to add them throught additional modules
    * to deploy a npm/yarn node based app ,dependencies must be installed on the server before unpacking the .zip/.tar/.. than run it
    * therefore the artifact along with the pachage.json must be copied to the server inorder to deploy the application
    * for nodejs apps the front/back-end can be packaged in the same artifact or packaged separetly   
    * code needs to be compressed to shorten loading page time and transpiled to ensure compatability with most browsers ,this can be achieved with special tools like "webpack" 
    * "webpack" traspiles ,minifies ,bundels and compress code
    * js-framework/java has a standerdized both front/back-end single artifact build wich is a best-practice unlike js-framework/nodejs wich is more flexible in choice
