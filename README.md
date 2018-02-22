# Proactive Load Balancing for Video Transcoding

Python application to implement proactive load balancing for transcoding video using video features

Packages used:
1. Python
2. Socket
3. SkLearn
4. Numpy
5. Bluelet

The application uses Support Vector Regression(SVR) for prediciting the transcoding time.

Reference Links:
1. http://scikit-learn.org/stable/modules/svm.html#svm 
2. http://scikit-learn.org/stable/auto_examples/svm/plot_svm_regression.html#example-svm-plot-svm-regression-py 
3. https://docs.python.org/2/library/socket.html 
4. https://github.com/sampsyo/bluelet 
5. http://ieeexplore.ieee.org/xpl/abstractKeywords.jsp?reload=true&arnumber=6890256 

For implementation, follow
Step 1- Run server1.py server2.py and server3.py pyton file 
step 2- Run tough_call.py
Step 3- Run sendfile_client.py

Details:
The process starts from the client side implementation. The client starts off by collecting ten random datasets from the actual dataset containing around 1 million data points. These collected data points are then encapsulated into an object of class video_request that contains all the parameters required to train the machine learning algorithm-SVR. These objects are then forwarded to the load balancer by establishing a connection using python sockets. The load balancer maintains this connection using a multi-threaded environment, that adds the functionality of accepting requests from multiple clients and process them concurrently. After accepting the request from the client, the load balancer sends this data for processing by making use of the machine learning algorithm.
The machine learning algorithm uses SVR(support vector regression) for predicting the transcoding time for videos that client is requesting for transcoding. SVR algorithm first trains data to create a regression function. The kernel involved for generating this function is radical base function. For training the kernel 1000 random points are gathered from the original dataset. These random data points are then converted to an numpy array i.e., a multi dimension array having values converted to the exponential values. These data points are then preprocessed using a scalar function. This scalar function converts the data point to values centered around the origin of the axis. The final dataset and the transcoding time for these final dataset is then trained using the rbf function. This function is then fed with data points sent by the client and the output of this function is the transcoding time.

Using this transcoding time, the load balancer allocates the load to the servers having higher available space and time and continues this process until all the load has been completely divided among the servers.
