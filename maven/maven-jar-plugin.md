





# 参考资料

```
<plugin>
	<groupId>org.apache.maven.plugins</groupId>
	<artifactId>maven-jar-plugin</artifactId>
	<version>2.4</version>
	<configuration>
		<archive>
			<!-- 生成的jar中，包含pom.xml和pom.properties这两个文件 -->
			<addMavenDescriptor>true</addMavenDescriptor>
			<!-- 生成MANIFEST.MF的设置 -->
			<manifest>
				<!--这个属性特别关键，如果没有这个属性，有时候我们引用的包maven库 
				下面可能会有多个包，并且只有一个是正确的，其余的可能是带时间戳的， 
				此时会在classpath下面把那个带时间戳的给添加上去，
				然后我们 在依赖打包的时候，打的是正确的，所以两头会对不上，报错。 -->
				<useUniqueVersions>false</useUniqueVersions>
				<!-- 为依赖包添加路径, 这些路径会写在MANIFEST文件的Class-Path下 -->
				<addClasspath>true</addClasspath>
				<!-- 这个jar所依赖的jar包添加classPath的时候的前缀，如果这个jar本身
				和依赖包在同一级目录，则不需要添加 -->
				<classpathPrefix>lib/</classpathPrefix>
				<!-- jar启动入口类 -->
				<mainClass>com.ht.pojo.Test</mainClass>
			</manifest>
			<manifestEntries>
				<!-- 在Class-Path下添加配置文件的路径 -->
				<Class-Path>../config/</Class-Path>
				<!-- 假如这个项目可能要引入一些外部资源，但是你打包的时候并不想把
				这些资源文件打进包里面，这个时候你必须在这边额外指定一些这些资源 
				文件的路径，这个位置指定的话，要根据你预期的这些位置去设置，我这边 
				所有jar都在lib下，资源文件都在config下，lib和config是同级的 
				同时还需要注意另外一个问题，假如你的pom文件里面配置了 
				<scope>system</scope>,就是你依赖是你本地的资源，这个时候使用 
				这个插件，classPath里面是不会添加，所以你得手动把这个依赖添加进 
				这个地方，用空格隔开就行 -->
			</manifestEntries>
		</archive>
		<!-- jar包的位置 -->
		<outputDirectory>${project.build.directory}/lib</outputDirectory>
		<includes>
			<!-- 打jar包时，打包class文件和config目录下面的 properties文件 -->
			<!-- 有时候可能需要一些其他文件，这边可以配置，包括剔除的文件等等 -->
			<include>**/*.class</include>
			<include>**/*.properties</include>
		</includes>
	</configuration>
</plugin>
```

