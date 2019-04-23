---
title: "Creating a Python Executable"
date: 2019-04-23
tags:
    - python
    - data science
published: true
header:
    # image: "/images/sanFran.jpg"
excerpt: "Data Science, Python Executable"
mathjax: "true"
toc: true
---

# Creating an Executable for a Python File
I thought I would write this article to help anyone else that had trouble with this when finishing up your python project.
Before discussing how to create an executable file of your project it might be helpful to give you some idea as to what an executable file actually is and how it is different from the python file you have already. So when programming any project in the python language or any other language, that file has a specific extension. For example, python files have the extension of .py which tells you and the computer that this is a python file and to be handled in that manner. This means that the python file with the extension of .py, needs to be run in an IDE or within the terminal. Yet, there is only so much that this file can do on its own, and is still dependent on the IDE to run the program.
This is where an executable file comes into play. An executable file, the the extension of .exe, allows the file to be run and do a task automatically. This means that the program you have can be converted into an executable file which would allow the computer to run the file and automatically complete operations or tasks programmed into the program without continued permission.

This article will now focus on how to convert your python files into an executable file to automatically run your program’s operations. The first step is finding the tool you would like to use to convert your python script to an executable. The one I’ll be using in this article is pyinstaller. Before beginning anything you will need to install the python tool. To do this use the line:

::pip install pyinstaller or conda install -c conda-forge pyinstaller::

One of these line will do the trick to install pyinstaller depending on your python environment.

From here, if you have just a one file script then just run :

::pyinstaller yourscript.py:::

This line will convert your python script into an executable. This is a very simple scenario and wasn’t the cause for me to determine the need for a complete layout for file structures that include more than just a script. For example I was creating an network GUI simulator so there was a python script and also png files that I was using as the background for the GUI. When running the above line, my images were not being located when I tried running my executable. What I had to do, was first create an .spec from my python script. How you do this is running the line :

::pyi-makespec yourscript.py::

Now when you return to your project directory you will see a .spec file. One thing I found that worked here is to go ahead and create and executable from your .spec file using :

::pyinstaller yourscript.spec::

We’ll come back to these other files created in just a minute.
Now open your .spec script in any simple text editor, and add the files you need added under datas in a= Analysis. An example of adding an image to the data looks like : 

::a.datas += [(‘Image.png’,’yourfiledirectorylocation’, "DATA")]::

Now that you have include your file in the executables data, it will have access to it during execution. But I found another problem after I thought this had fixed my problems. It was that my image was still not being located during the execution. I found out that there was an additional step to do with the image in your file. My lines of code looked like this before:

::image = Image.open(“Network_layer.png”)::
::photo_image = ImageTk.PhotoImage(image)::

The one change I needed to make was :

::image = Image.open(resource_path(“Network_layer.png”))::
::photo_image = ImageTk.PhotoImage(image)::

Adding the resource_path() finally fixed my problem. After this, save everything, then run the :

::pyinstaller yourscript.spec::

One more time to ensure the executable has updated with the additional information you are sending in during the running of the executable. Now you can run the executable and everything should work correctly. Feel free to reach out if you have any questions or if I have misinterpreted or got something wrong, always trying to learn something new! Thanks!
