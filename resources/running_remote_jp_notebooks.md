## Accessing code, data, and jupyter notebooks on the server from your laptop

Many of you might be working on a remote server where you have to use `vim` to write your code. Maybe some of you want to be able to access the remote server in a more convinient way. For example, you might want to work on jupyter notebooks on the server. Here is how I do it. 

### On the server side 

- `ssh` to the server  
- Go to the directory you want to access from the client, e.g., your laptop. 
- Run `jupyter-notebook` on your server:  

```
(py35) vkolhatk@Ling-DiscourseLab-GPU1:~/dev$ jupyter-notebook --no-browser --port=8899
[I 15:01:51.496 NotebookApp] JupyterLab beta preview extension loaded from /home/vkolhatk/anaconda3/envs/py35/lib/python3.5/site-packages/jupyterlab
[I 15:01:51.497 NotebookApp] JupyterLab application directory is /home/vkolhatk/anaconda3/envs/py35/share/jupyter/lab
[I 15:01:51.500 NotebookApp] Serving notebooks from local directory: /home/vkolhatk/dev
[I 15:01:51.500 NotebookApp] 0 active kernels
[I 15:01:51.500 NotebookApp] The Jupyter Notebook is running at:
[I 15:01:51.500 NotebookApp] http://localhost:8899/<YOUR_TOKEN>
[I 15:01:51.500 NotebookApp] Use Control-C to stop this server and shut down all kernels (twice to skip confirmation).
```
- Later you will use this URL to connect to the server. (When you connect for the first time, you will have to login with a token:
```http://localhost:8888/?token=<YOUR_TOKEN>)```

- Usually, I use the `nohup` command so that the jupyter notebook keeps running in the background on the server even when I end my  `ssh` session. 
```
(py35) vkolhatk@Ling-DiscourseLab-GPU1:~/dev$ nohup jupyter-notebook &
[1] 29276
(py35) vkolhatk@Ling-DiscourseLab-GPU1:~/dev$ nohup: ignoring input and appending output to 'nohup.out'

(py35) vkolhatk@Ling-DiscourseLab-GPU1:~/dev$
```

- That's all for the server side! 

### On the client side (e.g., your laptop)

- Do the `ssh` tunneling from your laptop with the following command. The port 8899 is for the server and 8890 is the local port for the client. 
```ssh -N -f -L localhost:8890:localhost:8899 <USERNAME>@<SERVER_NAME>```
- You will be prompted to enter the password for your server. 
- Go to your favourite browser on your laptop and enter the link with the token provided by the jypyter-server
```http://localhost:8890/?token=<YOUR TOKEN>```
- Enjoy accessing code, data, and jupyter notebooks on the server from your laptop! 
