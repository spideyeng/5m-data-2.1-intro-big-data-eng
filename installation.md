# Module 2 First-Time Software Installation

## Conda Environments

Install conda environments required for the rest of module. Go to the `environments` folder and create the conda environments based on the `environment.yml` file. Each `yml` file is prefixed with the environment name. 

For example, to create the `bde` environment, first navigate into the `environments` folder by running `cd environments`, then run the following command:

`conda env create --file bde-environment.yml`

To replace an existing environment:

`conda env update --file bde-environment.yml --prune`

### Environments

Create all the environments in the `environments` folder at this point. 

Here is where the environments will be used:
- `bde`: Lesson 2.1 onwards
- `elt`: Lesson 2.5 onwards
- `dagster`: Lesson 2.6 onwards
- `ooc`: Lesson 2.7
- `kafka`: Lesson 2.10

Please prepare your environments before each lesson. Reach out to your cohort of Discord if you have any questions.

### For Windows WSL Users

If you get an error message when creating the `bde` environment, e.g.
> ERROR: Could not build wheels for thriftpy2, which is required to install pyproject.toml-based projects.

Run the following CLI command from your terminal:

`sudo apt install build-essential`

## Preparation for Lesson 2.1

For lesson 2.1, you will need to setup MongoDB to demonstrate a NoSQL database.

### MongoDB

- Setup [instructions](https://drive.google.com/file/d/1XeQ8FE_exsdhMOF5kOn2bqoovLs0i7bS/view?usp=drive_link) for MongoDB. 
- [Video guide](https://drive.google.com/file/d/1lH2KBHvXollEsDCr1sCzFAAryE8-mnQy/view?usp=sharing) for setting up MongoDB.


## Preparation for Lesson 2.2

For lesson 2.2, you will need to setup user accounts on Redis and Google Cloud Platform (GCP).

### Redis
- Setup [instructions](https://drive.google.com/file/d/1n-DPX64e0WRH9nK58rL1Ig73wbtmI0ir/view?usp=drive_link) for Redis.
- [Video guide](https://drive.google.com/file/d/1YRNs7ezKNp2GvMBJxE8BuphRnjRIdJI-/view?usp=drive_link) for setting up Redis.

### GCP

- Setup [instructions](https://drive.google.com/file/d/1UlqE8E9si7ATKmj0mJn4zj4NMvOQODXa/view?usp=sharing) for GCP account.
- [Video guide](https://drive.google.com/file/d/1JaORL_1Lhmf-Xjp88o3Icw4L5ienJ2Ph/view?usp=drive_link) for setting up GCP Account.
- [Video guide](https://drive.google.com/file/d/1miz5Mp5cpo3KTvrXVwPoAc40ba3tUo2Q/view?usp=drive_link) for installing gcloud CLI.



