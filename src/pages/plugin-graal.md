---
title: Graal VM plugin
permalink: /plugins/graalvm.html
description: Plugin for using JavaScript with Apache Ant using the Graal VM.
layout: page
eleventyNavigation:
  key: plugin-graal
  parent: plugins
  title: Graal VM plugin
  excerpt: DITA-OT plugin providing the Graal VM for excecuting JavaScript with Apache Ant
preloads:
  href: '/assets/fonts/robotomono/robotomono-variablefont_wght-webfont.woff2'
  as: 'font'
  type: 'font/woff2'
  crossorigin: true
---

{% set crumbs = collections.all | eleventyNavigationBreadcrumb(eleventyNavigation.key) %}
{% for crumb in crumbs %}
Parent: <a class="crumb" href="{{ crumb.url | url }}">{{ crumb.title }}</a>
{% endfor %}

[<i class="fa-brands fa-github"></i> org.jung.graal](https://github.com/stefan-jung/org.jung.graal) is a plugin for the [DITA-OT](https://www.dita-ot.org/) and is providing the Graal VM for executing JavaScript with Apache Ant.

GraalVM is a high-performance JDK distribution designed to accelerate the execution of applications written in Java and other JVM languages along with support for JavaScript, Ruby, Python, and a number of other popular languages.


Installation
============

Install this plugin with the `dita` command.

```bash
dita install https://github.com/stefan-jung/org.jung.graal/archive/refs/heads/main.zip
```


Usage
=====

You can use the Apache Ant [**`<script>`**](https://ant.apache.org/manual/Tasks/script.html) task.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project name="MyProject" basedir="." default="main">

  <target name="main">
    <script language="javascript"> <![CDATA[
        // create and use a Task via Ant API
        echo = MyProject.createTask("echo");
        echo.setMessage("Hello World!");
        echo.perform();
    ]]></script>
  </target>

</project>
```

As an alternative, you can also use the [**`<scriptdef>`**](https://ant.apache.org/manual/Tasks/scriptdef.html) task to create custom Ant tasks.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project name="MyProject" basedir="." default="main">

  <scriptdef name="custom-echo" language="javascript">
    <attribute name="msg"/>
    <![CDATA[
      self.log(attributes.get("msg"));
    ]]>
  </scriptdef>

  <target name="main">
    <custom-echo msg="Hello World!"/>
  </target>
  
</project>
```

## Libraries

The libraries used in this plugin can be obtained from:

| Library             | Maven Repository                                                   |
|---------------------|--------------------------------------------------------------------|
| **commons-io**      | https://mvnrepository.com/artifact/commons-io/commons-io           |
| **js**              | https://mvnrepository.com/artifact/org.graalvm.js/js               |
| **js-scriptengine** | https://mvnrepository.com/artifact/org.graalvm.js/js-scriptengine  |
| **graal-sdk**       | https://mvnrepository.com/artifact/org.graalvm.sdk/graal-sdk       |
| **truffle-api**     | https://mvnrepository.com/artifact/org.graalvm.truffle/truffle-api |
| **icu4j**           | https://mvnrepository.com/artifact/com.ibm.icu/icu4j               |


## License

GraalVM Community Edition is open source and distributed under [version 2 of the GNU General Public License with the “Classpath” Exception](LICENSE), which are the same terms as for Java. The licenses of the individual GraalVM components are generally derivative of the license of a particular language (see the table below). GraalVM Community is free to use for any purpose - no strings attached.

Component(s) | License
------------ | -------------
[GraalVM Compiler](compiler/LICENSE.md), [SubstrateVM](substratevm/LICENSE), [Tools](tools/LICENSE), [VM](vm/LICENSE_GRAALVM_CE) | GPL 2 with Classpath Exception
[GraalVM SDK](sdk/LICENSE.md), [GraalWasm](wasm/LICENSE), [Truffle Framework](truffle/LICENSE.md), [TRegex](regex/LICENSE.md) | Universal Permissive License
