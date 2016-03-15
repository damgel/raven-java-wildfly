# raven-java-wildfly
A  class to act as a Wildfly custom logger with Raven. See [this thread](https://github.com/getsentry/raven-java/issues/140) for more info. 

If you are waiting for [this pull request](https://github.com/getsentry/raven-java/pull/174) to get merged, try this project.

standalone.xml [Jboss Logging Subsystem](https://docs.jboss.org/author/display/WFLY8/Logging+Configuration) configuration:

```xml
<custom-handler name="RAVEN" enabled="true" class="br.com.tecnobiz.raven.wildfly.SentryHandler" module="com.getsentry.raven">
    <level name="ERROR"/>
    <formatter>
        <named-formatter name="PATTERN"/>
    </formatter>
    <properties>
        <property name="dsn" value="https://<key>:<secret>@app.getsentry.com/<project>"></property>
        <property name="tags" value="tag1:value1,tag2:value2"></property>
    </properties>
</custom-handler>
```

Create a Wildfly Module:

```xml
<module xmlns="urn:jboss:module:1.0" name="com.getsentry.raven">
	<resources>
		<resource-root path="jackson-core-2.5.0.jar" />
		<resource-root path="guava-18.0.jar" />
		<resource-root path="raven-7.0.0.jar" />
		<resource-root path="raven-java-wildfly-1.0.0.jar" />
	</resources>
</module>
```

That's it.
