Hi all, Hope you all are doing good. Today's article is a really exciting one and focusses on how to use an openUI service called ollama and run something like chatGPT on your localhost. The end product could end up looking like the following

![[openui.png]]
*As you can see this is very familiar to chatgpt and by the end of this article you will be able to host something like this as well*

# Table of Contents
- [[#Install Ollama]]
- [[#Pulling an Ollama Image]]
- [[#Setting up WebUI]]
- [[#Using Ollama]]


## Install Ollama
Now depending on the Operating System there can be various methods for installation of Ollama. But for the sake of uniformity we are going to only use the linux curl command on all three Operating System. On windows this is possible by installing WSL which is Windows Subsystem for Linux. Learn how to do so on your WIndows machine by clicking [here](https://learn.microsoft.com/en-us/windows/wsl/install). 

Now that we are all on the same page installing ollama is really easy just input the below curl command to begin the installation process
```bash
curl -fsSL https://ollama.com/install.sh | sh
```
Once the installation is complete check ollama service by doing 
```bash
❯ curl localhost:11434
Ollama is running
```
*You will receive a response stating that Ollama is running*

### Pulling an Ollama Image
Ollama boasts a wide collection of language models all of which can be found over [here](https://ollama.com/library). 

Pulling an ollama image is as easy as pulling a docker image. You just input 
```bash
ollama pull <image_name>
```
*All the pull commands can also be found on the above provided link*

![[ollama_pull.png]]
*After Issuing the pull command wait for the download to complete*

To run the model run 
```bash
ollama run <model_name>
#Some other ollama commands
#Command to list all ollama Language Models
ollama ls
#Command to delete/remove a language model
ollama rm <model_name>
```

### Setting up WebUI
To Setup webui make sure you have docker installed on your operating system. Follow the guide [here](https://docs.docker.com/engine/install/) to install docker and return to this tutorial

Once docker is installed input the following docker command for installing the webUI
```bash
docker run -d --network=host -v open-webui:/app/backend/data -e OLLAMA_BASE_URL=http://127.0.0.1:11434 --name open-webui --restart always ghcr.io/open-webui/open-webui:latest
```
*this will pull the openUI latest image and serve it on localhost:8080*

### Using Ollama
#### CLI
To use ollama directly from CLI run 
```bash
ollama run <model_name>
```
![[ollama_cli.png]]
*Here you can see We are using Ollama direcly within our cli*

#### GUI
- Visit the browser at http://locahost:8080 
- Complete the signup process 
- Start using the GUI


![[ollama_gui.png]]

*The main feature of using openUI is that it can offer many more features such as choosing between many LLM's or the ability to upload files for context*
