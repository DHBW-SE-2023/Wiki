# Exploration Sprints

In the Exploration Sprints we tested critical software to ensure its implementation possibility.

The software bits we tested were: 
 - Mail Integration
 - Programming Language + Frontend Tool
 - afsa


 ## Mail Integration

 We created a simple code for demonstaion.

 ## Programming Language + Frontend Tool

 As we were flexible with the decision of which programming language to use we concentrated on their ability to connect to different frontend tools. The frontend tools which we chose to take a closer look at were Electron, Tauri and Fyne. 

The exploration sprint was completed if the coder was able to create a basic ui-window displaying a clickable button that executes a simple "Hello World" function in the backend.

We combined Electron with Python, however we decided against using this combination due to only finding deprecated libraries for our use cases.

Rust was tested with Tauri which was successful in its exploration sprint but the setup was difficult and the usage of Rust turled out to be unintuitive. Since we wanted to give Tauri another try, we used Python as programming language which eventually turned out to be a dead end as well. The reason for it was that we were unable to setup an environment where interoperation between Tauri and Python was possible.

The combination we chose to use in the end was Go and Fyne. Go is an open source programming language having a clean syntax and fast compile times. It is also designed for web development, packaging and multithreading which makes it a great choice to use for our project. The