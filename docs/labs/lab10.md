---
title: Lab 10
description: Testing Socket Programming
layout: default
date: 2021-11-15T17:00:00-6:00
# notes gets passed through markdownify
github_link: https://classroom.github.com/a/sMnT5xnJ
student_ports_link: https://docs.google.com/spreadsheets/d/1H5mTka0nY6K9PSaPWbSORM-vNSawGXW5ofVsP-zD5uk/edit?usp=sharing
gradescope_link: https://www.gradescope.com/courses/293389/assignments/1659129
man_page: https://man7.org/linux/man-pages/man1/curl.1.html
---
import Link from '@docusaurus/Link';
import site from '@site/course.json'

## Testing Socket Programming 

## Introduction to cURL 

The name cURL stands for "client URL".
The program is written in C and is used to transfer data into computer networks.
It allows developers to communicate with servers directly instead of having to go through a browser. 
Scripts based on cURL commands are used to automate processes, testing, and debugging. 
Refer Man Page of the <Link to={frontMatter.man_page}>curl</Link> for more details.
```bash
curl [options] <url>
```

## Testing with Script.

1.  Test the following script against your <Link to={frontMatter.github_link}>HomeWork5</Link> solution.
    Modify the PORT number in the script based on the PORT on which you are running the server.
    Note: create and run the script from homework5 folder.

    ```bash
    # test index
    curl -s http://localhost:5000 | diff - index.html
    # test basic "can the server receive a post message"
    curl -v http://localhost:5000/speak?hello+how+are+you -X POST 2>&1 | grep "HTTP/1.1 200 OK"
    # test whether listen receives that same post and spits it out correctly
    (curl -sN http://localhost:5000/listen > test_output) & X=$! ; (curl -X POST http://localhost:5000/speak?hello+how+are+you) ; sleep 3 ; kill $X
    ```

2.  Script will create `test_output` file. Ideal output content of the `test_output` should be as follow:

    ```    
    retry: 10000
    
    data: hello how are you 

    ```

Answer the <Link to={frontMatter.gradescope_link}>Gradescope</Link> Quiz based on your learning

## Running and Testing Web Server Code 

1.  If you are running in a Docker container evironment you can run and test
    your program locally. However, if you're using `systemsX`, you will need to
    forward ports from the systemsX machine to your local machine. The format
    for this command is:

    ```bash
    ssh -L localPort:localhost:remotePort netid@systemsX.cs.uic.edu
    ```
    which makes `http://localhost:remotePort` on `systemsX` accessible on your local machine at `http://localhost:localPort`.

    For instance, if you are  <Link to={frontMatter.student_ports_link}>assigned port</Link>  33000, and want to test your code
    locally, you can do so by connecting to `systems1` like so:

    ```
    ssh -L 33000:localhost:33000 netid@systems1.cs.uic.edu
    ```

    And then as long as that ssh session is connected, there is a "tunnel" that sends any connections made to your local computer at port 33000 on `systems1.cs.uic.edu`


## Total grade calculation

| Task | Points |
|---|---|
| Turn in the Gradescope assignment | 5 points |
| Total points | 5 points |
