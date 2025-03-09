text 

# Docker Lambda Layer

Open Docker and in the terminal type 

**Pull the latest Ubuntu image**

```
docker pull ubuntu:latest
```

Create a new container with this image.

```
docker run -it --name duckdb ubuntu:latest /bin/bash
```

Update

```
apt update && apt upgrade
```

**Install python and pip**

```
apt install -y software-properties-common
```

You will be asked some options about location - it’s ok to select anything here.

Check the Python version.

```
python3 --version
```

In case you need to install another version of python! 

Steps

Install pip

```
apt install -y python3-pip
```

**Install aws-cli.**

```
apt install -y curl unzip zip less
```

Download the aws-cli installation script.

```
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
```

Run the installer

```
unzip awscliv2.zip && ./aws/install

aws --version
```

**Step 4: Install required libraries and package the lambda layer.**

Create a new directory for the installation.

```
mkdir python && cd python/
```

Install the duck-db library.

```
pip install duckdb -t .
```

Package your lambda layer

```
cd ..
zip -r duckdb1.1.3-3.12-layer.zip python
```

Configure the default region, secret key, and secret access key

```
aws configure
```

Key ID:

Secret:

Default region: eu-north-1

Deploy the lambda

```
aws lambda publish-layer-version --layer-name duckdb1_1_3-3_12-layer --zip-file fileb://duckdb1.1.3-3.12-layer.zip --compatible-runtimes python3.12

```

Layer name can only include:

- Letters (`a-z`, `A-Z`)
- Numbers (`0-9`)
- Hyphens ()
- Underscores (`_`)
