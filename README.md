# psta-web-user-tomcat-config
custom tomcat external config to add `allowTrace` property in server.xml

[cf official docs: container-tomcat](https://github.com/cloudfoundry/java-buildpack/blob/main/docs/container-tomcat.md#additional-resources)

### Additional Resources
The container can also be configured by overlaying a set of resources on the default distribution.  To do this follow one of the options below.

#### Buildpack Fork
Add files to the `resources/tomcat` directory in the buildpack fork.  For example, to override the default `logging.properties` add your custom file to `resources/tomcat/conf/logging.properties`.

#### External Tomcat Configuration
Supply a repository with an external Tomcat configuration.

Example in a manifest.yml

```yaml
env:
  JBP_CONFIG_TOMCAT: '{ tomcat: { external_configuration_enabled: true }, external_configuration: { repository_root: "http://repository..." } }'
```

The artifacts that the repository provides must be in TAR format and must follow the Tomcat archive structure:

```
tomcat
|- conf
   |- context.xml
   |- server.xml
   |- web.xml
   |...
```

Notes:
* It is required the external configuration to allow symlinks. For more information check [Tomcat 7 configuration] or [Tomcat 8 configuration].
* `JasperListener` is removed in Tomcat 8 so you should not add it to the server.xml.
