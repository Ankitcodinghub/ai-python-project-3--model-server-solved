# ai-python-project-3--model-server-solved
**TO GET THIS SOLUTION VISIT:** [AI-python Project 3- Model Server Solved](https://www.ankitcodinghub.com/product/python-p3-6-of-grade-model-server-solved/)


---

📩 **If you need this solution or have special requests:** **Email:** ankitcoding@gmail.com  
📱 **WhatsApp:** +1 419 877 7882  
📄 **Get a quote instantly using this form:** [Ask Homework Questions](https://www.ankitcodinghub.com/services/ask-homework-questions/)

*We deliver fast, professional, and affordable academic help.*

---

<h2>Description</h2>



<div class="kk-star-ratings kksr-auto kksr-align-center kksr-valign-top" data-payload="{&quot;align&quot;:&quot;center&quot;,&quot;id&quot;:&quot;119422&quot;,&quot;slug&quot;:&quot;default&quot;,&quot;valign&quot;:&quot;top&quot;,&quot;ignore&quot;:&quot;&quot;,&quot;reference&quot;:&quot;auto&quot;,&quot;class&quot;:&quot;&quot;,&quot;count&quot;:&quot;1&quot;,&quot;legendonly&quot;:&quot;&quot;,&quot;readonly&quot;:&quot;&quot;,&quot;score&quot;:&quot;5&quot;,&quot;starsonly&quot;:&quot;&quot;,&quot;best&quot;:&quot;5&quot;,&quot;gap&quot;:&quot;4&quot;,&quot;greet&quot;:&quot;Rate this product&quot;,&quot;legend&quot;:&quot;5\/5 - (1 vote)&quot;,&quot;size&quot;:&quot;24&quot;,&quot;title&quot;:&quot;AI-python Project 3- Model Server Solved&quot;,&quot;width&quot;:&quot;138&quot;,&quot;_legend&quot;:&quot;{score}\/{best} - ({count} {votes})&quot;,&quot;font_factor&quot;:&quot;1.25&quot;}">

<div class="kksr-stars">

<div class="kksr-stars-inactive">
            <div class="kksr-star" data-star="1" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="2" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="3" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="4" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="5" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
    </div>

<div class="kksr-stars-active" style="width: 138px;">
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
    </div>
</div>


<div class="kksr-legend" style="font-size: 19.2px;">
            5/5 - (1 vote)    </div>
    </div>
Overview

In the last project, you trained a simple PyTorch model using SGD. Now, you’ll write a program that can load a model (similar to the one from P2) and use it to make predictions upon request (this kind of program is called a model server).

Your model server will use multiple threads and cache the predictions (to save effort when the server is given the same inputs repeatedly).

You’ll start by writing your code in a Python class and calling the methods in it. By the end, though, your model server will run in a Docker container and receive requests over a network (via gRPC calls).

Learning objectives:

Use threads and locks correctly

Cache expensive compute results with an LRU policy

Measure performance statistics like cache hit rate

Communicate between clients and servers via gRPC

Before starting, please review the general project directions.

Corrections/Clarifications

Sept 30: Match up test_prediction_cache.py and test_modelserver.py with specification Sept 30: Update Testing section

Sept 30: Add additional Predict test case in docker_autograde.py

Sept 30: Add comments in autograde.py

Sept 30: Use -Request and -Response in modelserver.proto

Oct 02: Reword hit/miss rate to hit and miss rate (your hit rate is the number of hits divided by the total number of calls)

Oct 03: Added –break-system-packages to installation command

Oct 05: Increased time that autograder waits for server to bootup to 5 seconds

Part 1: Prediction Cache

PredictionCache class

Write a class called PredictionCache with two methods: SetCoefs(coefs) and Predict(X) in a file called server.py.

SetCoefs will store coefs in the PredictionCache object; coefs will be a PyTorch tensor containing a vertical vector of float32s.

Predict will take a 2D tensor and use it to predict y values (which it will return) using the previously set coefs, like this:

y = X @ coefs

In Python, a return statement can have multiple values; in this case it should have two:

1. the predict y values

2. a bool, indicating whether PredictionCache could make the prediction using a cache (see below)

Caching

Add code for an LRU cache to your PredictionCache class. Requirements:

Predict should round the X values to 4 decimal places before using them for anything

(https://pytorch.org/docs/stable/generated/torch.round.html); the idea is to be able to use cached results for inputs that are approximately the same

The cache should hold a maximum of 10 entries

Whenever SetCoefs is called, invalidate the cache (meaning clear out all the entries in the cache) because we won’t expect the same predictions for the same inputs now that the model itself has changes

The second value returned by Predict should indicate whether there was a hit

When adding an X value to a caching dictionary or looking it up, first convert X to a tuple, like this: tuple(X.flatten().tolist()). The reason is that PyTorch tensors don’t work as you would expect as keys in a Python dict (but tuples do work)

Use test_prediction_cache.py and verify that it produces the expected output indicated by the comments.

Locking

There will eventually be multiple threads calling methods in PredictionCache simultaneously, so add a lock.

The lock should:

be held when any shared data (for example, attributes in the class) are modified get released at the end of each call, even if there is an exception

Part 2: Model Server

Protocol

Read this guide for gRPC with Python:

https://grpc.io/docs/languages/python/quickstart/ https://grpc.io/docs/languages/python/basics/

Install the tools (be sure to upgrade pip first, as described in the directions):

shell pip3 install grpcio==1.58.0 grpcio-tools==1.58.0 –break-system-packages

Create a file called modelserver.proto containing a service called ModelServer. Specify syntax=”proto3″; at the top of your file. ModelServer will contain 2 RPCs:

1. SetCoefs

Request: coefs (repeated float)

Response: error (string)

2. Predict

Request: X (repeated float)

Response: y (float), hit (bool), and error (string)

You can build your .proto with: shell python3 -m grpc_tools.protoc -I=. –python_out=. –grpc_python_out=. modelserver.proto Verify modelserver_pb2_grpc.py was generated.

Server

Add a ModelServer class to server.py that inherits from modelserver_pb2_grpc.ModelServerServicer.

ModelServer should override the two methods of ModelServerServicer and use a PredictionCache to help calculate the answers. You’ll need to manipulate the data to translate back and forth between the repeated float values from gRPC and the tensors in the shapes needed by

PredictionCache. Although PredictionCache.Predict can work on multiple rows of X data at once, the X values received by ModelServer should be arranged as a single row.

The error fields should contain the empty string “” when all is well, or an error message that can help you debug when there was an exception or other issue (otherwise exceptions happening on the server side won’t show up anywhere, which makes troubleshooting difficult).

Start your server like this:

python import grpc from concurrent import futures server =

grpc.server(futures.ThreadPoolExecutor(max_workers=4), options=((‘grpc.so_reuseport’, 0),))

modelserver_pb2_grpc.add_ModelServerServicer_to_server(ModelServer(), server) server.add_insecure_port(” [::]:5440″, ) server.start() server.wait_for_termination()

You can do this directly in the bottom of your server.py, or within a main function; feel free to move imports to the top of your file if you like.

Use test_modelserver.py after starting the server to verify that it produces the expected output indicated by the comments.

Part 3: Client

Write a gRPC client named client.py that can be run like this:

python3 client.py &lt;PORT&gt; &lt;COEF&gt; &lt;THREAD1-WORK.csv&gt; &lt;THREAD2-WORK.csv&gt; …

For example, say you run python3 client.py 5440 “1.0,2.0,3.0” x1.csv x2.csv x3.csv.

For this example, your client should do the following, in order:

1. Connect to the server at port 5440.

2. Call SetCoef with [1.0,2.0,3.0].

3. Launch three threads, each responsible for one of the 3 CSV files.

4. Each thread should loop over the rows in its CSV files. Each row will contain a list of floats that should be used to make a Predict call to the server. The threads should collect statistics about the numbers of hits and misses.

5. The main thread should call join to wait until the 3 threads are finished.

The client can print other stuff, but its very last line of output should be the overall hit rate. For example, if the hit and total counts for the three threads are 1/1, 0/1, and 3/8, then the overall hit rate would be (1+0+3) / (1+1+8) = 0.4.

Part 4: Deployment

You should write a Dockerfile to build an image with everything needed to run both your server and client. Your Docker image should:

Build via docker build -t p3 .

Run via docker run -p 127.0.0.1:54321:5440 p3 (i.e., you can map any external port to the internal port of 5440)

You should then be able to run the client outside of the container (using port 54321), or use a docker exec to enter the container and run the client with port 5440.

Submission

You should organize and commit your files such that we can run the code in your repo like this:

shell python3 -m grpc_tools.protoc -I=. –python_out=. –grpc_python_out=. modelserver.proto python3 autograde.py

Tester

Run python autograde.py to get your score, which contains the following tests:

1. docker_build_run (10)

docker image builds and can start running

2. run_docker_autograde (0)

It starts the docker autograder (within the docker container)

3. protobuf_interface (10)

interface matches spec

4. set_coefs (10)

is correct, no errors

5. predict (10)

get expected result

6. predict_single_call_cache (10)

repeated call will hit cache

7. predict_full_cache_eviction (10)

repeated call will not hit cache after cache fills up

8. set_coefs_cache_invalidation (10)

cache is invalidated after SetCoefs

9. client_workload_1 (10) no repeats/cache_hits

10. client_workload_2 (10) LRU check

11. client_workload_3 (10) handles multiple CSVs

We will check the following:

Client uses threads

Server uses threads Server locking is correct Etc.
