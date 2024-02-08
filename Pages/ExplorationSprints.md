# Exploration Sprints

In the Exploration Sprints we tested critical software to ensure its implementation possibility.

The software bits we tested were: 
 - Image Processing
 - Mail Integration
 - Frontend Tool (+ Programming Language)

---

## Backend

The project's key technology is part of the backend. There we tested both image processing software and the mail integration.

### Image Processing

As image processing is the main background task, is has to be realizable in the chosen programming language. From the required steps of image processing (listed [here](ImageProcessing.md)) we concluded that if the first three steps are implementable, the other ones will be as well. Therefore, we chose the following as requirements for the image processing exploration sprint:

- Paper sheet detection
- Reverse perspective transform
- Table detection

The first prototype was implemented in OpenCV, which uses the programming language Python. As we were not sure whether we want to code in Python or in Go, it was necessary to also test image processing there. The working solution uses the library called GoCV.

Both technologies were compared in a juxtaposition to figure out the better solution of both.

In terms of Performance, Go at least on paper takes the lead since it is a compiled language and therefore links directly to the OPEN CV C++ library. The actual efficiency benefits compared to python aren't as big as they are on paper - they rather are more or less similar regarding their "execution" time [(source)](https://www.reddit.com/r/golang/comments/p5n05s/gocv_vs_opencv_python_performance/). Consequently, the point performance shouldn't matter as much, especially since the performance won't be the biggest problem for our "small" program.

Regarding the documentation, GO seems to be quite good "monitored" and has a big range of different functionalities similar to Python [(see here)](https://pkg.go.dev/gocv.io/x/gocv#section-documentation).
So therefore the main difference is the amount of help and support that can be found on the internet, if any problems occur. Given that OPEN CV has a huge amount of projects and users working with Python, the better choice in this point would be Python. 

(A big advantage of of Go concerning Parallelism and Concurrency is, that Go has built-in support for concurrent programming through go routines, which can be advantageous for real-time computer vision applications. You can easily implement parallel processing for image or video streams in Go.
In Python, its Global Interpreter Lock (GIL) can limit the ability to leverage multiple CPU cores effectively for parallel processing. To achieve parallelism, you may need to use external libraries or workarounds like multiprocessing. This point mentioned will not be needed for the YAAC project, therefore it is more or less irrelevant.)

In conclusion, both programming languages are suitable for the project as both fulfill the requirements of the exploration sprint. Therefore, the decision is a question of "Design" and "Usability". The modular design of Go works well especially for small "Fullstack/Web Applications". On the other hand, the importance of online support should not be underestimated, where Python would be the better choice.


### Mail Integration

The set measurable requirements for the mail integration exploration sprint were the following:
- Check if attachments can be extracted from Mails
- Check if Mails can be filtered by "Betreff" (Reference)
- (Move E-Mails, Mark them as read)

There were different approaches regarding the main integration. The most natural mail integration handling would have been if we had been able to get access to the DHBW's local network and mail client. This approach was quickly deprecated as it was not possible for us to get administration rights due to data privacy and information security reasons.

The second approach was to test alternatives using our student email addresses. The idea was to send the lists to a separate mail address that can be interfaced or to use WebScraper for OutlookWeb. Connecting to the DHBW server using IMAP protocol failed as it is unsupported. It turned out a success to connect to an IMAP supported email server in python and as the exploration sprint showed it is easily achievable as well.

____

## Programming Language + Frontend Tool

As we were flexible with the decision of which programming language to use we concentrated on their ability to connect to different frontend tools. The frontend tools which we chose to take a closer look at were Electron, Tauri and Fyne while the programming languages were Python, Rust and Go. The requirements for the frontend exploration sprint were the following:

- Cross Platform
- Implement a button with backend handling -> Execution of a simple function in backend
- Display "Hello World" text

We combined Electron with Python, however we decided against using this combination due to only finding deprecated libraries for our use cases.

Rust was tested with Tauri which was successful in its exploration sprint but the setup was difficult and the usage of Rust turned out to be unintuitive. Since we wanted to give Tauri another try, we used Python as programming language which eventually turned out to be a dead end as well. The reason for it was that we were unable to setup an environment where interoperation between Tauri and Python was possible.

The combination we chose to use in the end was Go and Fyne. Go is an open source programming language having a clean syntax and fast compile times. It is also designed for web development, packaging and multithreading which makes it a great choice to use for our project.

---

## Conclusion

The exploration sprints helped us to find the technologies we needed for the project. By implementing basic, but nevertheless important functions of the project, we were able to determine the pros and cons of each aspect.

The chosen technologies are Go, Fyne, AND MORE.

