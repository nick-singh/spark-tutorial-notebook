# How To Install Spark

Installing Spark and getting to work with it can be a daunting task.
This section will go deeper into how you can install it and what your options are to start working with it.

First, check if you have the Java [jdk](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) installed. Then, go to the Spark download page. Keep the default options in the first three steps and you’ll find a [downloadable](https://spark.apache.org/downloads.html) link in step 4. Click to download it.

Next, make sure that you untar the directory that appears in your “Downloads” folder. Next, move the untarred folder to `/usr/local/spark`.

```
$ mv spark-2.1.0-bin-hadoop2.7 /usr/local/spark 
```

Now that you’re all set to go, open the README file in `/usr/local/spark`. You’ll see that you’ll need to run a command to build Spark if you have a version that has not been built yet. So, make sure you run the command:

```
 $ build/mvn -DskipTests clean package run
```

This might take a while, but after this, you’re all set to go!

#### Running Spark Applications Using Jupyter Notebooks

When you have downloaded a Spark distribution, you can also start working with Jupyter Notebook. If you want to try it out first, go [here](https://try.jupyter.org/) and make sure you click on the “Welcome to Spark with Python” notebook. The demo will show you how you can interactively train two classifiers to predict survivors in the Titanic data set with Spark MLlib.

There are various options to get Spark in your Jupyter Notebook: you can run PySpark notebooks in your Docker container, you can set up your Jupyter Notebook with Spark or you can make sure you add a kernel to work with it in your notebook.

In any case, make sure you have the Jupyter Notebook Application ready. If you don’t, consider installing [Anaconda](https://www.continuum.io/downloads), which includes the application, or install it with the help of `pip pip3 install jupyter`. 

##### Spark in Jupyter Notebook

Now that you have all that you need to get started, you can launch the Jupyter Notebook Application by typing the following:

```
PYSPARK_DRIVER_PYTHON="jupyter" PYSPARK_DRIVER_PYTHON_OPTS="notebook" pyspark
```

Or you can launch Jupyter Notebook normally with jupyter notebook and run the following code before importing PySpark:

```
pip install findspark 
```

With findspark, you can add pyspark to sys.path at runtime. Next, you can just import pyspark just like any other regular library:

```
import findspark
findspark.init()

# Or the following command
findspark.init("/path/to/spark_home")

from pyspark import SparkContext, SparkConf
```

Note that if you haven’t installed Spark with brew and in accordance with the instructions that are listed above, it could be that you need to add the path to SPARK_HOME to `findspark.init()`. If you’re still in doubt where `SPARK_HOME` is located at, you can call `findspark.find()` to automatically detect the location of where Spark is installed.

Tip: you can read more about `findspark` [here](https://github.com/minrk/findspark).


##### Jupyter Notebook with Spark Kernel

Next, if you want to install a kernel, you want to make sure you get Apache Toree installed. Install Toree via pip with `pip install toree`. Next, install a jupyter application `toree`:

```
jupyter toree install --spark_home=/usr/local/bin/apache-spark/ --interpreters=Scala,PySpark
```

Make sure that you fill out the `spark_home` argument correctly and also note that if you don’t specify `PySpark` in the interpreters argument, that the Scala kernel will be installed by default. This path should point to the unzipped directory that you have downloaded earlier from the Spark download page. Next, verify whether the kernel is included in the following list:

```
jupyter kernelspec list
```

Start Jupyter notebook as usual with `jupyter notebook` or configure Spark even further with, for example, the following line:

```
SPARK_OPTS='--master=local[4]' jupyter notebook 
```

In which you specify to run Spark locally with 4 threads.
