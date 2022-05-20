## Note: The repository credits goes to Noah Gift. I replicated it while reading the book - Practical MLOps from O'Reily. 

# flask-ml-azure-serverless
Deploy Flask Machine Learning Application on Azure App Services

![continuous-delivery](https://user-images.githubusercontent.com/58792/85061538-f7352780-b174-11ea-8001-b0561c5bad73.jpg)

## To run it locally follow these steps

1.  Create virtual environment and source

```bash
python3 -m venv ~/.flask-ml-azure
source ~/.flask-ml-azure/bin/activate
```

2.  Run `make install`

3.  Run `python app.py`

4.  In a separate shell run: `./make_prediction.sh`

## To run it in Azure Pipelines

1.  Refer to [Azure Official Documentation guide here throughout](https://docs.microsoft.com/en-us/azure/devops/pipelines/ecosystems/python-webapp?view=azure-devops)

2. Launch Azure Shell  

![1-launch-azure-shell](https://user-images.githubusercontent.com/58792/89555246-cc169e00-d7dd-11ea-8164-88caa1b8beba.png)

3.  Create Github Repo with Azure Pipelines Enabled (Could be a fork of this repo)

![2-create-Github-Repo](https://user-images.githubusercontent.com/58792/89555912-a3db6f00-d7de-11ea-9d2f-5ac030b43ec9.png)

4. Clone the repo into Azure Cloud Shell

*Note:  You make need to follow this YouTube video guide on how to [setup SSH keys and configure cloudshell environment](https://www.youtube.com/watch?v=3vtBAfPjQus)*

5.  Create virtual environment and source

```bash
python3 -m venv ~/.flask-ml-azure
source ~/.flask-ml-azure/bin/activate
```

2.  Run `make install`

3.  Create an app service and initially deploy your app in Cloud Shell

`az webapp up -n <your-appservice>`

![3-flask-ml-service](https://user-images.githubusercontent.com/58792/89557009-2e709e00-d7e0-11ea-9b31-9090c8067a10.png)

4. Verify deployed application works by browsing to deployed url: `https://<your-appservice>.azurewebsites.net/`

You will see this output:

![4-deployed-app](https://user-images.githubusercontent.com/58792/89557343-a8088c00-d7e0-11ea-891c-4d88333b8097.png)

5.  Verify Machine Learning predictions work

Change the line in `make_predict_azure_app.sh` to match the deployed prediction
`-X POST https://<yourappname>.azurewebsites.net:$PORT/predict `

![5-successful-prediction](https://user-images.githubusercontent.com/58792/89557573-02a1e800-d7e1-11ea-8318-1c628e13dae7.png)

6. [Create an Azure DevOps project and connect to Azure, (as official documentation describes)](https://docs.microsoft.com/en-us/azure/devops/pipelines/ecosystems/python-webapp?view=azure-devops)

![6-devops](https://user-images.githubusercontent.com/58792/89558313-097d2a80-d7e2-11ea-8b65-df052b300331.png)

7.  Connect to Azure Resource Manager

![7-service-connection](https://user-images.githubusercontent.com/58792/89558869-d0918580-d7e2-11ea-8ffe-52cfaf95fe16.png)

8.  Configure connection to previously deployed resource group

![8-azure-pipelines-setup](https://user-images.githubusercontent.com/58792/89560149-988b4200-d7e4-11ea-9e25-3554ac2bd8fd.png)

9.  Create new Python Pipeline with Github Integration

![9-newpipeline](https://user-images.githubusercontent.com/58792/89560429-f750bb80-d7e4-11ea-9f85-241d65d25c55.png)

![10-github-integration](https://user-images.githubusercontent.com/58792/89560627-5282ae00-d7e5-11ea-8b0b-bdecfff0e4d3.png)


This process will create a YAML file that looks roughly like the YAML output shown below.  Refer to azure-pipelines in the repo

10.  Verify Continuous Delivery of Azure Pipelines by changing `app.py`

![Continuous-Delivery](screenshot_CD.png)





