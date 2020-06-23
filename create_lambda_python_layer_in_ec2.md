Install latest Python (e.g. 3.8.2), if necessary ([ref](https://www.ntweekly.com/2020/02/16/install-python-3-8-on-amazon-linux-2-ec2-instance/)). The latest version can be fund at https://www.python.org/downloads/source/.

```
# yum install gcc openssl-devel bzip2-devel libffi-devel

# cd /opt
# sudo wget https://www.python.org/ftp/python/3.8.34/Python-3.8.3.tgz
# sudo tar xzf Python-3.8.3.tgz

# cd Python-3.8.3/
# sudo ./configure --enable-optimizations
# sudo make altinstall

# python3.8
```

Install Python packages in target directory, compress, and upload into S3.

```
# pip3.8 install aws-xray-sdk -t ./python
# zip -r layer.zip ./python
# aws s3 cp layer.zip s3://<SOME_S3_BUCKET>/layer.zip
# aws lambda publish-layer-version \
  --layer-name python38-aws-xray-sdk \
  --compatible-runtimes python3.8 \
  --content S3Bucket=<SOME_S3_BUCKET>,S3Key=layer.zip
```
