- *This is the copy of my question at [StackOverflow](https://stackoverflow.com/questions/56892720/developing-in-java-ide-locally-but-building-and-deploying-remotely)*
- *This is the source of the [diagram](https://github.com/pozdneev/draw.io/blob/master/Remote%20Java%20Development.drawio)*
- *This might be a solution https://habr.com/ru/post/510210/*

# Developing in Java IDE locally, but building and deploying remotely
This is the development environment configuration I need:

[![Remote web development][1]][1]

  [1]: https://i.stack.imgur.com/5V5NA.png

This development environment consists of **two parts:**

- **IDE client** that runs on a local computer (Linux, macOS, Windows)
- **IDE server** that runs on a remote computing server (Linux)

The development environment has the following **features:**

- The workspaces contain Java source files and are synchronized by the IDE via `rsync` or a similar tool when a developer clicks <kbd>Build</kbd> in the IDE client
- The compilation happens remotely (it might also happen locally for quick checks, but the war/jar-files are not directly transferred via the network)
- The war-file is deployed to a remote web server that runs on a remote computing server
- The jar-files (*not shown on the image*) run on a remote computing server
- The log files from a remote web server (and from the jars) are accessible in real time in the IDE client on a local computer

I would like to develop in Java locally, but be able to build and deploy remotely, because I have the following **limitations:**

- My primary database lives on a remote computing server (I also have a rarely synchronized local database replica that I use for quick checks)
- The web server and jars have to be located on the same computing server as the database, because their interaction with the database is very intensive (I also have a local web server for quick checks; it interacts with the local database replica)
- The jar file produces a highly compute intensive workload and I prefer to not run it locally
- My war/jar files are rather large, the network bandwidth is rather low and the latency is rather high, so I would like to build on the server (otherwise, I would need to wait several minutes to copy the war/jar files from local machine to the computing server)
- Because of the above-mentioned network properties:

  - I can hardly rely on mounting a server's workspace locally
  - The Remote Desktop session is slow

My current solution is the following:

- I synchronize workspaces by means of a version control system (`git`) that runs on a third-party server (*not shown on the image*)
- I connect to the remote computing server using Remote Desktop and run the IDE there

I strongly believe that Eclipse, NetBeans, or Intellij IDEA might have the functionality that I described. However, none of the links I found cover my scenario:

- [Remote C/C++ development in CLion](https://www.jetbrains.com/help/clion/remote-projects-support.html)
- [Deploying remotely in Intellij IDEA](https://www.jetbrains.com/help/idea/creating-a-remote-server-configuration.html)
- [Remote C/C++ development in Eclipse](https://help.eclipse.org/luna/index.jsp?topic=%2Forg.eclipse.ptp.rdt.doc.user%2Fhtml%2Fconcepts%2Foverview.html)
- [Developing embedded applications with NetBeans](https://netbeans.org/kb/docs/java/javase-embedded.html)

Any ideas on how to configure a development environment that I described?
