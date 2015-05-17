---
layout: default
---

# Getting Started

To make neural nets run with Deeplearning4j, there are configuration prerequisites documented on the [ND4J.org "Getting Started" page](http://nd4j.org/getstarted.html):

1. [Java](http://nd4j.org/getstarted.html#java) 
2. [Integrated Development Environment](http://nd4j.org/getstarted.html#ide-for-java) 
3. [Maven](http://nd4j.org/getstarted.html#maven)
4. [Canova](http://nd4j.org/getstarted.html#canova)
5. [Github](http://nd4j.org/getstarted.html#github)

After that, please read the following:

5. OS-specific instructions
    * <a href="#linux">Linux</a>
    * <a href="#osx">OSX</a>
    * <a href="#windows">Windows</a>
6. <a href="#source">Working With Source</a>
7. <a href="#eclipse">Eclipse</a>
8. <a href="#trouble">Troubleshooting</a>
9. <a href="#next">Next Steps</a>

### <a name="linux">Linux</a>

* Due to our reliance on Jblas for CPUs, native bindings for Blas are required.

        Fedora/RHEL
        yum -y install blas

        Ubuntu
        apt-get install libblas* (credit to @sujitpal)

* If GPUs are broken, you'll need to enter an extra command. First, find out where Cuda installs itself. It will look something like this

         /usr/local/cuda/lib64

Then enter *ldconfig* in the terminal, followed by the file path to link Cuda. Your command will look similar to this

         ldconfig /usr/local/cuda/lib64

If you're still unable to load Jcublas, you will need to add the parameter -D to your code (it's a JVM argument):

         java.library.path (settable via -Djava.librarypath=...) 
         // ^ for a writable directory, then 
         -D appended directly to "<OTHER ARGS>" 

If you're using IntelliJ as your IDE, this should work already. 

### <a name="osx">OSX</a>

* Jblas is already installed on OSX.  

### <a name="windows">Windows</a>

* Install [Anaconda](http://docs.continuum.io/anaconda/install.html#windows-install). If your system doesn't like the default 64-bit install, try the 32-bit offered on the same download page. (Deeplearning4j depends on Anaconda to use the graphics generator matplotlib.) 

* Install [Lapack](http://icl.cs.utk.edu/lapack-for-windows/lapack/). (Lapack will ask if you have Intel compilers. You do not.)

* To do so, you will need to install [MinGW 32 bits](http://www.mingw.org/) even if you have a 64-bit computer (the download button is on the upper right), and then download the [Prebuilt dynamic libraries using Mingw](http://icl.cs.utk.edu/lapack-for-windows/lapack/#libraries_mingw). 

* Lapack offers the alternative of [VS Studio Solution](http://icl.cs.utk.edu/lapack-for-windows/lapack/#lapacke). You'll also want to look at the documentation for [Basic Linear Algebra Subprograms (BLAS)](http://www.netlib.org/blas/). 

* Alternatively, you can bypass MinGW and jcopy the Blas dll files to the right path. For example, the path to the MinGW bin folder is: /usr/x86_64-w64-mingw32/sys-root/mingw/bin.

* Cygwin is not supported. You must install DL4J from DOS Windows.  

* Once you've completed these steps, you're ready to start solving problems with Deeplearning4j. 

###<a name="source">Working With Source</a>

We highly recommend downloading the [Deeplearning4j JAR files from Maven Central](https://search.maven.org/#search%7Cga%7C1%7Cdeeplearning4j), rather than working with source, unless you plan on making significant commits to the project (which are always welcome, of course). To download from Maven, please follow the [intructions on the ND4J site](http://nd4j.org/getstarted.html#maven).

For a deeper dive, check out our [Github repo](https://github.com/SkymindIO/deeplearning4j/). If you want to develop for Deeplearning4j, install Github for [Mac](https://mac.github.com/) or [Windows](https://windows.github.com/). Then git clone the repository, and run this command for Maven:

      mvn clean install -DskipTests -Dmaven.javadoc.skip=true

If you want to run Deeplearning4j examples after installing from trunk, you should git clone ND4J, Canova and Deeplearning4j, respectively, and then install all from source using Maven with this command:

      mvn clean install -DskipTests

If you receive a Javadoc error, run this:

      mvn clean install -DskipTests -Dmaven.javadoc.skip=true

Following these steps, you should be able to run the 0.0.3.3 examples. 

###<a name="eclipse">Eclipse</a> 

After running a git clone, enter this command

      mvn eclipse:eclipse 
  
which will import the source and set everything up. 

### <a name="trouble">Troubleshooting</a>

* If you have installed DL4J before and now see the examples throwing errors, run a git clone on [ND4J](http://nd4j.org/getstarted.html) in the same root directory as DL4J; run a clean Maven install within ND4J; install DL4J again; run a clean Maven install within DL4J, and see if that fixes things.
* When you run an example, you may get a low [f1 score](../glossary.html#f1), which is the probability that the net's classification is accurate. In this case, a low f1 doesn't indicate poor performance, because the examples train on small data sets. We gave them small data sets so they would run quickly. Because small data sets are less representative than large ones, the results they produce will vary a great deal. For example, on the minuscule example data, our deep-belief net's f1 score currently varies between 0.32 and 1.0. 
* Deeplearning4j includes an **autocomplete function**. If you are unsure which commands are available, press any letter and a drop-down list like this will appear:
![Alt text](../img/dl4j_autocomplete.png)
* Here's the Javadoc for all [Deeplearning4j's classes and methods](http://deeplearning4j.org/doc/).
* Some problems you encounter using DL4J may be due to a lack of familiarity with the ideas and techniques of machine learning. We strongly encourage all Deeplearning4j users to rely on resources beyond this website to understand the fundamentals. Andrew Ng's watershed [machine-learning lectures on Coursera](https://www.coursera.org/course/ml) are a great place to start. [Geoff Hinton's neural nets course](https://www.youtube.com/watch?v=S3bx8xKpdQE), available on Youtube, is also instructive. While we've partially documented DL4J, many parts of the code are essentially a raw domain-specific language for deep learning. 

### <a name="next">Next Steps: MNIST and Running Examples</a>

Take a look at the [MNIST tutorial](../mnist-tutorial.html). 

When you're building a new project with Deeplearning4j, you'll create a new project, following the instructions on the ND4J ["Getting Started"](http://nd4j.org/getstarted.html) page and including the dependencies you need in your POM file as shown [here](http://nd4j.org/dependencies.html). 

Once you do that, you can open up the App.java file that is created with every new project, and start writing DL4J code between the curly brackets you see after **public static void main( String[] args )**. 

For example, try pasting a Multilayer model like the one in the Mnist tutorial cited above. Many of the classes will appear in red, since you haven't imported the right packages, but IntelliJ will add those packages automatically to the top of your file if you press Alt+Return while your mouse hovers over the missing class in the code. 

If you have a clear idea of how deep learning works and what you want to build, go straight to our section on [custom datasets](../customdatasets.html). 