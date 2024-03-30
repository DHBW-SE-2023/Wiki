# Documentation for this repository
The [YAAC code documentation](https://pkg.go.dev/github.com/DHBW-SE-2023/YAAC) documents all packages from the main branch. You find the specific code files in the directories section for most of the code you must enable "show internal" to see the documentation as per default internal documentation is not visible.

# Guide to document code in this project with Godoc

[Godoc reference](https://go.dev/blog/godoc) 

[Godoc CLI](https://pkg.go.dev/golang.org/x/tools/cmd/godoc#pkg-overview) 

## Add to your project
```
go install golang.org/x/tools/cmd/godoc@latest
```

## How to use
### online
You can add your repository (using open source license) to ```https://pkg.go.dev/<URL>``` using the *URL* to your repository.
Trigger a scan and it will appear. Make sure you **set an open source licence** before triggering the scan as you can not easily trigger a re-scan.
For example the *go-prototype* repository can be found here: https://pkg.go.dev/github.com/DHBW-SE-2023/yaac-go-prototype

### local
Godoc starts a web server and presents the documentation as website. 
Run
```
godoc -http=:8080
```
choosing the port using ```-http:<port>``` and ```-goroot=<pathToYourProject>``` for your project.
If you want to see the hole project structure you need to add go to your package and add a ```?m=all``` to your url.

## What is Godoc
**Godoc** automatically parses source code and comments to *html*.
It uses normal language comments as base not any other constructs.
It is a minimal code documentation framework that can easily be implemented.
For your comments to be interpreted by Godoc you should_
* Place your comments directly above the element (everything from structs to packages) you want to describe with **no line in between**
* Start the sentence with the element you describe so that the comment can be understood even without looking at the underlying source code
* If the described entity is deprecated (not longer used but needed for compatibility reasons) a paragraph starting with **Deprecated** has to be written

# Guide to create code diagrams with go-callvis

[Calvis reference](https://pkg.go.dev/github.com/truefurby/go-callvis#section-readme)

[Go-calvis github](https://github.com/ondrajz/go-callvis)

## Add to your project
```
go install github.com/ofabry/go-callvis@latest
```

## How to use
```
go-callvis -file <pathToTargetFile> <pathToTargetPackage>
```
The default output is an *.svg* file which can be viewed in browsers or specialized software.
For output in other formats please specify the format using ```-format=<svg|png|jpg|...>```
