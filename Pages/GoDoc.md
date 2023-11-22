# Guide to ducumenting code in this project with Godoc

[Godoc reference](https://go.dev/blog/godoc) 

[Godoc CLI](https://pkg.go.dev/golang.org/x/tools/cmd/godoc#pkg-overview) 

## Add to your project
```
go install golang.org/x/tools/cmd/godoc@latest
```

## How to use
Godoc starts a web server and presents the documentation as website. 
Run
```
godoc -http=:8080 -goroot=$HOME/go
```
choosing the port using *-http:[port]* and *-goroot=[pathToYourProject]* for your project

## What is Godoc
**Godoc** automatically parses source codeand comments to *html*.
It uses normal language comments as base not any other constructs.
It is a minimal code documentation framework that can easily be implemented.
For your comments to be interpreted by Godoc you should_
* Place your comments directly abouve the element (everything from structs to packages) you want to describe with **no line in between**
* Start the sentence with the element you describe so that the comemnt can be understood even without looking at the underlying source code
* If the entity you are describing is depricated(not longer used but needed for compatibility reasons) write a paragraph starting with **Deprecated**
