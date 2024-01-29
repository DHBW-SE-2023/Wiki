# Exploration Sprints

In the Exploration Sprints we tested critical software to ensure its implementation possibility.

The software bits we tested were: 
 - Programming Language + Frontend Tool
 - Image Processing
 - Mail Integration



 ## Programming Language + Frontend Tool

 As we were flexible with the decision of which programming language to use we concentrated on their ability to connect to different frontend tools. The frontend tools which we chose to take a closer look at were Electron, Tauri and Fyne. 

The exploration sprint was completed if the coder was able to create a basic ui-window displaying a clickable button that executes a simple "Hello World" function in the backend.

We combined Electron with Python, however we decided against using this combination due to only finding deprecated libraries for our use cases.

Rust was tested with Tauri which was successful in its exploration sprint but the setup was difficult and the usage of Rust turled out to be unintuitive. Since we wanted to give Tauri another try, we used Python as programming language which eventually turned out to be a dead end as well. The reason for it was that we were unable to setup an environment where interoperation between Tauri and Python was possible.

The combination we chose to use in the end was Go and Fyne. Go is an open source programming language having a clean syntax and fast compile times. It is also designed for web development, packaging and multithreading which makes it a great choice to use for our project.



## Backend

The project not only consists of frontend and user interface. Therefore we also had to test the backend which consists of image processing and mail integration.

### Image Processing

As image processing is the main background task, is has to be realisable in the chosen programming language. From the required steps of image processing we concluded that if the first three stages are implementable, the other steps will be as well. Therefore, we chose the following steps as requirements for the image processing exploration sprint:

- Paper sheet detection
- Reverse perspective transform
- Table detection

The first prototype was implemented in OpenCV, which uses the programming language Python. As we chose Go in the Frontend exploration sprint, it was necessary to also make image processing work in Go. The working solution is called GoCV, which is 


On paper GO obviously has a better performance, since it is a compiled language and therefore it links directly to the OPEN CV C++ library. But from what I've seen and read, the actual efficiency benefits compared to python aren't as big. Both are more or less similar regarding their "execution" time.
So in my opinion this point shouldn't matter as much, since the performance won't be the biggest problem for our "small" program.

Documentation and Support

Regarding the documentation, GO seems to be quite good "monitored" and has a big range of different functionalities similar to Python.(https://pkg.go.dev/gocv.io/x/gocv#section-documentation)
So therefore the main difference is the amount of help and support we'll find in the internet, if any problems occur. Given that OPEN CV has a huge amount of projects and users working with Python, I'd say that we'll be better of with Python.

Parallelism and Concurrency

"Go: Go has built-in support for concurrent programming through goroutines, which can be advantageous for real-time computer vision applications. You can easily implement parallel processing for image or video streams in Go.
Python: Python's Global Interpreter Lock (GIL) can limit the ability to leverage multiple CPU cores effectively for parallel processing. To achieve parallelism, you may need to use external libraries or workarounds like multiprocessing."

=> Regarding the Point mentioned above, this seems to be a big advantage of GO, but as far as I can see, we won't need that. So this is more or less irrelevant.

Conclusion

On MAC OS the main functionalities are running without any problems so far.
I'll dive a bit deeper and keep this issue updated, if there will be any problems.

So as far as I can see, it's more or less a question of "Design" and "Usability".
Personally I feel like Go might be more usable, due to it's modular design especially for small "FullStack/Web Applications".
But at the same time I believe, we shouldn't underestimate the importance of "Support".(Python Bigger Community)

Besides that I couldn't yet check if GOCV provides all of the functions, that we'll need for the signature detection. But I've read some posts suggesting that GOCV regularly misses higher level functions/modules.

### Mail Integration