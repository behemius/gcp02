# gcp02
3 hosts MariaDB Galera Cluster on Google Cloud Compute Engine free tier.

Free Tier in GCP
----------------
1 non-preemptible f1-micro VM instance per month in one of the following US regions:

Oregon: us-west1
Iowa: us-central1
South Carolina: us-east1

30 GB-months HDD

5 GB-month snapshot storage in the following regions:
Oregon: us-west1
Iowa: us-central1
South Carolina: us-east1
Taiwan: asia-east1
Belgium: europe-west1

1 GB network egress from North America to all region destinations (excluding China and Australia) per month

Preparation
-----------

Google Cloud Shell: 

git clone https://github.com/behemius/gcp02.git 

gcloud config set project behemius


Installation example clean VM (for 'behemius' project)
-------------------------------------------------------

Creation: 

gcloud deployment-manager deployments create mariadb --config gcp02/test_vm.yaml

Deletion: 

gcloud deployment-manager deployments delete mariadb

Parameters:
- service: Compute v1 instance
- machine: f1-micro
- zone: us-west1-a
- OS: Debian 10

Installation MariaDB:
sudo apt install mariadb-server -y


Installation node1 VM (for 'behemius' project)
----------------------------------------------
It's modification example clean VM.
There is used dedicated internal IP (10.138.0.11) and installed MariaDB

Creation: 

gcloud deployment-manager deployments create mariadb --config gcp02/test2_vm.yaml

Deletion: 

gcloud deployment-manager deployments delete mariadb

Installation cluster (for 'behemius' project)
---------------------------------------------

Google Cloud Shell:

git clone https://github.com/behemius/gcp02.git
gcloud config set project behemius

Creation: 

gcloud deployment-manager deployments create galera --config gcp02/cluster.yaml

Deletion: 

gcloud deployment-manager deployments delete galera

Parameters:
- Default subnet: 10.138.0.0/20
- IP addresses: 10.138.0.11-13

