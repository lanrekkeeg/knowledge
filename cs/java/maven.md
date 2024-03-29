
# Maven

## Parallel builds

```
mvn -T 4  clean install    # will use 4 threads
mvn -T 1C clean install    # will use 1 thread per available CPU core
mvn -T 1.5C clean install  # will use 1.5 thread per CPU core
```

## Build necessary modules only

```
-pl, --projects
        Build specified reactor projects instead of all projects
-am, --also-make
        If project list is specified, also build projects required by the list
```

So just cd into the parent directory and run:

```
mvn clean install -pl <module> -am
```

## Random notes

```
# skip tests ;-)
mvn clean install -DskipTests

# force to update dependencies
mvn clean package -U
```
