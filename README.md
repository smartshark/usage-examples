# Using the SmartSHARK Database Release

This repository explains how to use our database releases such that you can create your own analysis scripts. Below, we descripe how our data can be loaded and how to run a sample analysis in Python with [Jupyter Lab](https://jupyter.org/install). 

## Preparation of the Database

First, you need to prepare a local database for analysis. 

- Download a release of the SmartSHARK MongoDB from Zenodo. [You can find a list of releases on our Website](https://smartshark.github.io/dbreleases/). 
- Then, you must prepare the MongoDB instance where you want to host the data. Make sure you install the version that we used for the database backup, which is listed on the Website together with the Link to Zenodo. Otherwise, you may have compability issues. A guide on how to setup a fresh MognoDB can be found [here](https://docs.mongodb.com/manual/installation/#install-mongodb).
- Run [mongorestore](https://docs.mongodb.com/database-tools/mongorestore/) to load the data into your local database.

For example, on Ubuntu 18.04 you can achieve all this as follows for release 1.0 of the database. 

```
wget -O smartshark_1_0.agz https://zenodo.org/record/4071449/files/smartshark_1_0.agz?download=1
wget -qO - https://www.mongodb.org/static/pgp/server-4.0.asc | sudo apt-key add -
echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu bionic/mongodb-org/4.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.0.list
sudo apt-get update
sudo apt-get install -y mongodb-org
sudo systemctl daemon-reload
sudo systemctl start mongod
wget https://user.informatik.uni-goettingen.de/~sherbol/smartshark_sample.agz
mongorestore --gzip --archive=smartshark_sample.agz
```

## Running the Notebook

To run our python, you only need our library [pycoshark](https://github.com/smartshark/pycoSHARK) and [Jupyter Lab](https://jupyter.org/install) (or any other app, that can work with Jupyter Notebooks). 

For example, you could run the following commands in your Ubuntu 18.04 machine to get everything running.

```
sudo apt-get install python3-venv build-essential python3-dev
git clone https://github.com/smartshark/usage-examples
cd usage-examples/
python3 -m venv venv
source venv/bin/activate
pip install pycoshark jupyterlab
```

You can just open the notebook in the browser and run our example.
