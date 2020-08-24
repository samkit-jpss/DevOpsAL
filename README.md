DevOps is a set of practices that combines software development and IT operations. It aims to shorten the systems development life cycle and provide continuous delivery with high software quality. DevOps is complementary with Agile software development.
![image](https://user-images.githubusercontent.com/56602504/91017900-7844eb00-e60c-11ea-978f-f40430f82672.png)

I’ve created a project where I’ve managed to create a DevOps Environment and complete automation from end to end workflow. Here I’ve mentioned title as DevOps AL. Many of you might we wondering what does AL meant here? DevOps Assembly Line which is pipeline of pipelines. Let’s understand what dose pipeline means first. The core of a DevOps pipeline constitutes the following: Continuous Integration & Continuous Delivery (CI/CD), continuous testing (CT), continuous deployment, continuous monitoring, continuous feedback, and continuous operations.
In this project I’ve tried to use as much DevOps tools as I can.
![image](https://user-images.githubusercontent.com/56602504/91017963-8b57bb00-e60c-11ea-8af0-72d62460b192.png)

Overview
1 .In this project a Developer writes a code for a website and I happend to be that Developer.
2 .Then he pushes the code to the the Source Control Management (SCM) for example here I used GitHub.
3. Jenkins automatically comes to know that code has been uploaded by the developer using GitHub web-hooks or you can also use Poll SCM . Hence , it pulls the complete code and copies the code in one folder. Then it launches some monitoring tool such as prometheus and visualizing tool such as grafana for monitoring. You can download the Dockerfile of these tools from my Docker repository : Prometheus , Grafana
4.After the code has been copied Quality Assurance Team (QAT) performs various testing such as unit testing , integration testing , acceptance test and many more.
5. If everything works fine and approved by QAT , finally it is deployed to the production and website is visible to our clients.
Image for post
Let’s see how’s it done!
I’ve used Jenkins pipeline as a plugin to run all the jobs in just one click. For that you have to download pipeline plugin from manage plugins.
![image](https://user-images.githubusercontent.com/56602504/91018006-9e6a8b00-e60c-11ea-8e6b-ae042bb3f594.png)

Stage View of Complete Assembly Line
![image](https://user-images.githubusercontent.com/56602504/91018068-b7733c00-e60c-11ea-8b9d-58ae7db5b768.png)
Devloper:
After writing the code I’ve pushed the code in the GitHub.
![image](https://user-images.githubusercontent.com/56602504/91018188-e5f11700-e60c-11ea-9f51-cdb8a49808b6.png)
Jenkins Pipeline (Job1):
After pushing the code Jenkins will run Jobs which I’ve created. First it pulls the code from the GitHub and copies the code in one folder. Also I’ve written one python code which sends the message automatically only if the build or this jobs runs.
![image](https://user-images.githubusercontent.com/56602504/91018258-fb664100-e60c-11ea-933a-335903f6138b.png)
Message Received, which keeps on telling us which process is running..
![image](https://user-images.githubusercontent.com/56602504/91018298-09b45d00-e60d-11ea-9118-95cb933e8157.png)

Jenkins Pipeline (JOB2):
This job2 runs prometheus and grafana on the top of Kubernetes and I’ve created a deployment for both of them also I’ve created a PVC so that we don’t loose the data and If the by chance any pod gets destroyed kubernetes will automatically launches another one.
I’ve already made a complete article on this which you can find Here.

Also we can see that the deployment has been launched :
![image](https://user-images.githubusercontent.com/56602504/91018407-2ea8d000-e60d-11ea-9268-fc6aab8926a5.png)

This Job runs only if the job1 runs perfectly and if it runs successfully we get a mail for its completion.

Jenkins Pipeline JOB3:
As testing the code is the import part . We might wanna test the code manually if everything works well or not. If everything is perfect QAT approved the code for the deployment.
As it asks for the approval first :

![image](https://user-images.githubusercontent.com/56602504/91018486-484a1780-e60d-11ea-80b4-a3e35a752d1a.png)

Finally our website has been deployed

![image](https://user-images.githubusercontent.com/56602504/91018536-55670680-e60d-11ea-9297-6ffc729ff5cf.png)
