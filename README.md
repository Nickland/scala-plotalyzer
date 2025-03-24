# Plotalyzer

This is the sibling program to the [appanalyzer](https://github.com/simkoc/scala-appanalyzer). 
The plotalyze will assist with evaluating the collected information during app analysis via a plugin system.
You can use and install already known plugins using the plugin manager or you can write your own.
Each plugin provides its own unique capability of analyzing the collected data and outputting them in a human readable form, usually json.


## Requirements

- Java 17


## Build

Go into the project root and run:

```
$> sbt stage
```

Move  `/resources/db.example.json` to `/resources/db.json` and adjust the values according to your local postgres configuration for the database
containing the appanalyzer experiments you want to analyze.

## Use

The `./run.sh` forms the command line interface. Use the `-h` flag to orientate yourself. 

## Writing your own plugin

To write your own plugin you need to depend on this repository. It is publicly available

```
ThisBuild / resolvers ++= Seq(
  "Sonatype OSS Snapshots" at "https://s01.oss.sonatype.org/content/repositories/public",
)
libraryDependencies ++= Seq("de.halcony" %% "plotalyzer" %% "1.1.0") 
```

you then need to implement the `AnalysisPlugin` interface. Move the packaged jar of your project into the plugin folder
to make the plugin locally available.

Running the plugins is done via:

```
$> run.sh analysis <experiment-id> <path-to-desired-output-file> <name-of-plugin>
```