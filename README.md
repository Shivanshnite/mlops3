# MLOPS Task 3

### Tired of tweaking and waiting for your classification models to be perfect, here is how you automate them using ***JENKINS*** + ***DOCKER*** + ***GITHUB***

# How to use this project :
- Put your data for ML model structured as follows :
  - ***Data***
    - class1
      - class1_1.jpg
      - class1_2.jpg 
      - . . .
      - . . .
      - class1_n.jpg
    - class2
      - class2_1.jpg
      - class2_2.jpg 
      - . . .
      - . . . 
      - class2_n.jpg
    - . . .
    - . . .
    - . . . 
    - classm
      - classm_1.jpg
      - classm_2.jpg 
      - . . . 
      - . . . 
      - classm_n.jpg

- Run the get_model.py script 
- ***VIOLA*** its done, now **sit back and wait for the mail, that the best model is trained**

## The setup we wil do below will automatically train different variations of your model and output the best possible model !

# Pre - requisites
- Basics of Docker
- Basics of Linux Operating System
- Basics of Jenkins
- I am assuming you have already set up Docker and Jenkins in your OS and has given ***root privileges to jenkins user***, if not, then do the following

```
echo "jenkins        ALL=(ALL)       NOPASSWD: ALL" >> etc/sudoers
```

# SETUP :

- Copy the ***get_model.py*** , ***make_model.py*** and ***modify_model.py*** from this repo 
- Create a github repo for your project and add **make_model.py*** , ***modify_model.py*** and ***get_model.py*** to it
- Now go to your home directory and clone the project using **git clone**
- We will be using tensorflow with docker, follow the official documentation to set up your docker to run tensorflow https://www.tensorflow.org/install/docker


**Now let's create our jobs and jenkins**


# TASK :

- [ ] 1.  Create container image that has Python3 and Keras or numpy  installed  using dockerfile 


- [ ] 2.	Create a job chain of job1, job2, job3, job4 and job5 using build pipeline plugin in Jenkins 


- [ ] 3.	 Job1 : Pull  the Github repo automatically when some developers push repo to Github.


- [ ] 4.	 Job2 : By looking at the code or program file, Jenkins should automatically start the respective machine learning software installed interpreter install image container to deploy code  and start training( eg. If code uses CNN, then Jenkins should start the container that has already installed all the softwares required for the cnn processing).


- [ ] 5.	Job3 : Train your model and predict accuracy or metrics.


- [ ] 6.	Job4 : if metrics accuracy is less than 80%  , then tweak the machine learning model architecture and retrain it.


- [ ] 7.	Job5: Notify that the best model is being created


- [ ] 8.	Create One extra job job6 for monitor : If container where app is running. fails due to any reason then this job should automatically start the container again from where the last trained model left



# TASK 1 : 

- [ ] 1.  Create container image that has Python3 and Keras or numpy  installed  using dockerfile 

- Copy the Dockerfile from tihs repo and paste it into a new dir

 ```
 mkdir /paste_docker_file_in_this_new_repo
 cd paste_docker_file_in_this_new_repo/
 docker build -t tf:v5 . 
 ```
 - Now we have an Image named tf:v5
 
 ( The image might take a little time to pull from docker hub )
 
 
# TASK 2 :  Create a job chain of job1, job2, job3, job4 and job5 using build pipeline plugin in Jenkins 

- [ ] ***JOB 1*** : Pull  the Github repo automatically when some developers push repo to Github.

- This is easy, make a new job named ***pull_from_github***

*** IMGE HERE***


- [ ] ***JOB 2*** : By looking at the code or program file, Jenkins should automatically start the respective machine learning software installed interpreter install image container to deploy code  and start training( eg. If code uses CNN, then Jenkins should start the container that has already installed all the softwares required for the cnn processing).

( we are making classification model using Transfer Learning for now, so all we need is to start the ***tf:v5*** we built )

- Make a new job named ***run_the_container*** and add the following

***Image here***


- [ ] ***JOB 3*** : Train your model and predict accuracy or metrics.

Here we will train the initial model made by user

***Image here***

- [ ] ***JOB 4*** : if metrics accuracy is less than 80%  , then tweak the machine learning model architecture and retrain it

*I am using a python script to manage all this so the complex part is already handled  by it*


- [ ] ***JOB 5*** : Notify that the best model is being created

*We will mail the user, notifying that the best model is trained, which can be found in ***jenkinsDownload*** folder along with history file


***Image here***

- [ ] ***JOB 6*** : Create One extra job job6 for monitor : If container where app is running. fails due to any reason then this job should automatically start the container again from where the last trained model left

- **We will check is the container is working or not, if not re-run the JOB 2**





