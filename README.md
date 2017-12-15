# Tide Local

[![License: GPL v2](https://img.shields.io/badge/License-GPL%20v2-blue.svg)](https://www.gnu.org/licenses/old-licenses/gpl-2.0.en.html)


## Dependencies  

* [Composer](https://getcomposer.org/)  
* [Docker](https://docs.docker.com/engine/installation/)  
* [Git](https://git-scm.com/)  
* *nix bash shell (Mac Terminal or suitable alternative for Windows)    
* AWS account for SQS queue and S3 buckets  

## Cloning `tide-local`
Ensure that you are in a folder where you would like to install the Tide services.

```
git clone -b develop --recursive https://github.com/wptide/tide-local.git tide-local
```

### Change to Tide working directory  

```
cd tide-local
```

### Update submodules  

```
git submodule update --init --recursive
```

## Hosts configuration

### *unix Environment

From a new terminal on the host machine:  

```
sudo cp /private/etc/hosts /private/etc/hosts-backup
sudo nano /private/etc/hosts
```

Use the arrow keys to navigate to the bottom of the hosts file and add a new host name.  

```
127.0.0.1 tide.local
```

When finished, hit `Control+O` followed by `ENTER/RETURN` to save changes to `/private/etc/hosts`, then hit `Control+X` to exit out of nano.


### Windows Environment

Add `tide.local` to your hosts file following this guide (see your specific version of Windows):   https://support.rackspace.com/how-to/modify-your-hosts-file/ 

## Composer Install  

```
services/api/bin/composer
```

## Alternative Composer (Windows)  

```
cd services/api
composer install
cd wp-content/plugins/wp-tide-api
composer install
```

## AWS setup  

Setup AWS IAM credentials with limited permissions for SQS & S3 access  
https://aws.amazon.com/documentation/iam/

Set Up an SQS queue (preferably FIFO)  
https://aws.amazon.com/documentation/sqs/ 

Setup S3 bucket with IAM  
https://aws.amazon.com/documentation/s3/

## .env configuration

Copy the `.env.dist` file to `.env`.  

```
cp .env.dist .env
```

Update placeholder values in `.env` to reflect your environment. For example, Tide API specific details; AWS key pairs; SQS queues and S3 buckets.

## Docker Containers

### Start Services

This will take a while and download several Docker images. Fast Internet access recommended as this will download roughly 1GB of image data to your host machine.

```
docker-compose up --build
```

### Stop Services

```
docker-compose down
```

### Start Polling SQS for Audits

```
docker-compose exec audit-server php bin/console tide:audit-server --env=dev -v
```

## Local URLs

* Front-End: [https://tide.local](https://tide.local)  
* Back-End: [https://tide.local/wp-admin/](https://tide.local/wp-admin/) `user:pass` are `admin`  

## References  

* [wptide/api](https://github.com/wptide/api)  
* [wptide/audit-server](https://github.com/wptide/audit-server)  
* [wptide/sync-server](https://github.com/wptide/sync-server)  

## Props  

[@valendesigns](https://github.com/valendesigns), [@rheinardkorf](https://github.com/rheinardkorf), [@danlouw](https://github.com/danlouw)  
