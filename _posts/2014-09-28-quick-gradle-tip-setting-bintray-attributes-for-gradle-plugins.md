---
layout: post
title: Quick Gradle Tip - Setting Bintray Attributes for Gradle Plugins
guid: 5005ed49e4b0d534734f5630:5005f070e4b0ee36c463b555:54289a90e4b0b8d209dc07e3
category: technical
tags:
    - gradle
    - build
---
As part of the new [Gradle plugin portal](http://plugins.gradle.org), you need to set some attributes on the version of your plugin package in Bintray.

The [Bintray Gradle plugin](https://github.com/bintray/gradle-bintray-plugin) lets you set attributes, so you can add the following snippet into your project to include all of your plugin IDs in the attributes.

Since Gradle requires you to put a properties file in your JAR for each plugin, you can get derive your whole attribute value from the project's group, name, and the names of the properties files within META-INF.

```groovy
def pluginIds = project.fileTree(
    dir: 'src/main/resources/META-INF/gradle-plugins',
    include: '*.properties').collect { file -> file.name[0..(file.name.lastIndexOf('.') - 1)] }

bintray {
    // ...
    pkg {
        // ...
        version {
            // ...
            attributes = ['gradle-plugin': pluginIds.collect { pluginId ->
                "${pluginId}:${project.group}:${project.name}" }]
        }
    }
}
```
