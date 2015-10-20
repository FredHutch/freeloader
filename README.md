Freeloader
==========

Freeloader is a simple web application (flask) that allows researchers 
to take advantage of HPC best practices to offer a compute pipeline
to collaborators. Design goals are:

 - ensure that only compute resources are used that are otherwise idle
 - ensure that the lowest cost storage is used to accompish the job 
 - limit security risks by offering minimal options for user input 
 - minimal impact on IT support 

# Implementation 

The application is developed in Python using the flask microframework.
The incoming file should be handed off to research python code that 
resides in a dedicated py file. 


## Features

 - Each pipeline will be offered under a dedicated URL
 - The only user interface will be a text field for an email address 
   and a file uploader for one or multiple files 
   (e.g. https://blueimp.github.io/jQuery-File-Upload/angularjs.html)
 - When the user hits the submit button the data could be scanned for 
   viruses or PII content before it is handed of to the computational 
   research code that then submits hpc jobs. 
 - when the computation has ended the result is copied to swift and made 
   available as a hidden file/link on the portal. The link has a configurable 
   expiration date
 - an email is sent to the collaborator that contains a link to the result
   file 


## Configuration details 

 - no NFS to writable shared file systems can be mounted on the webserver 
 - only the HPC restart queue is going to be used (jobs are preempted within
   seconds should there be a resource conflict. 
 - no posix file systems to store data. Input data will be stored in a Swift 
   object store that can be accessed via S3 or native Swift API. 
 - No authentication is provided. 


## Phase II

 - checkpoint restart. Jobs would be started with DMTCP checkpointing.
   Checkpoints are stored at regular intervals in persistent scratch 
   file systems
 - an app that provides generic large file upload services to researchers
   to avoid issues with 3rd party upload tools which are not fully integrated. 

