# Guide to ducumenting code in this project with Godoc

[Godoc reference](https://go.dev/blog/godoc) 

[Godoc CLI](https://pkg.go.dev/golang.org/x/tools/cmd/godoc#pkg-overview) 

## Add to your project
```
go install golang.org/x/tools/cmd/godoc@latest
```

## How to use
### online
You can add your repository (using open source licence) to ```https://pkg.go.dev/<URL>``` using the *URL* to your repository.
Trigger a scan and it will appear. Make sure you **set an open source licence** before triggering the scan as you can not easily trigger a rescan.
For example the *go-ptototype* repository can be found here: https://pkg.go.dev/github.com/DHBW-SE-2023/yaac-go-prototype

### local
Godoc starts a web server and presents the documentation as website. 
Run
```
godoc -http=:8080
```
choosing the port using ```-http:<port>``` and ```-goroot=<pathToYourProject>``` for your project.
If you want to see the hole project structure you need to add go to your package and add a ```?m=all``` to your url.

## What is Godoc
**Godoc** automatically parses source codeand comments to *html*.
It uses normal language comments as base not any other constructs.
It is a minimal code documentation framework that can easily be implemented.
For your comments to be interpreted by Godoc you should_
* Place your comments directly abouve the element (everything from structs to packages) you want to describe with **no line in between**
* Start the sentence with the element you describe so that the comemnt can be understood even without looking at the underlying source code
* If the entity you are describing is depricated(not longer used but needed for compatibility reasons) write a paragraph starting with **Deprecated**

# Guide to create code diagramms with go-callvis

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
The dafault output is an *.svg* file which can be viewd in browsers or specialized software.
For output in other formats please specify the format using ```-format=<svg|png|jpg|...>```


Back to main page [here](https://github.com/DHBW-SE-2023/Wiki/blob/main/README.md).