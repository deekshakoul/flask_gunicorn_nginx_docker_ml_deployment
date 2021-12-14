# Template to configure flask + gunicorn + nginx + docker
Check other [repository](https://github.com/deekshakoul/Production-Deployment-ML-Model) for deployment using flask, gunicorn and nginx

### Folder structure ###
![](others/docker.png)


<details><summary> Step 1 - installing docker and docker-compose </summary>
 ```
  [ Docker installation](https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository)
  [Install Compose on Linux systems](https://docs.docker.com/compose/install/#install-compose-on-linux-systems)
 ```
  
</details>


<details><summary>Step 2 - Docker image for Flask </summary>
  ```
.
├── flask_app 
   ├── app.py          
   ├── connector.py
   ├── models/
   ├── templates/
   └── **Dockerfile**
```
* Create a flask app - app.py, a WSGI interface - connector.py.
* A model folder that contains files related to your ML model and templates folder that conatins index.html which renders UI fro our ML model.
* Both the above points have already been covered [here.](https://github.com/deekshakoul/Production-Deployment-ML-Model)  
* New thing - Dockerfile
  * Create a docker image for flask - Dockerfile
  * Create a requirements.txt that will cotain all the packages that need to be installed - flask, gunicorn, gensim.
</details>

<details><summary> Step 3 - Web container(Nginx web server)  </summary>
```
├── nginx
   ├── nginx.conf          
   ├── project.conf
   └── Dockerfile  
```
 * nginx.conf - basic configuration setup file of nginx( can be found in /etc/nginx/)
 * project.conf - this is our nginx config setup file. Quite similar to what was done in earlier [repo](https://github.com/deekshakoul/Production-Deployment-ML-Model). The change to note here is argument **proxy_pass** which is set now as ` http://flask_app:8000;`, thus, pointing your Nginx configuration to the flask project. Since the flask container is called flask_app (in Step 2.)
    * This file also metions the port at which finally our app will run i.e port 80
</details>
