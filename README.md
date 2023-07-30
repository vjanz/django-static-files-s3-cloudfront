# django-static-files


## Setup & Installation

Create a virtual environment and install the dependencies:

```bash
$ python -m venv venv
$ source env/bin/activate

$ pip install -r requirements.txt
```

## Usage

### Collect static files

Create a new S3 Bucket and CloudFront distribution and then fill up the variables in settings.py.

```bash
DEBUG = False
AWS_ACCESS_KEY_ID = '<YOUR_AWS_ACCESS_KEY_ID>'
AWS_SECRET_ACCESS_KEY = '<YOUR_AWS_SECRET_ACCESS_KEY>'
AWS_STORAGE_BUCKET_NAME = '<YOUR_AWS_STORAGE_BUCKET_NAME>'
AWS_S3_CUSTOM_DOMAIN = f'{AWS_STORAGE_BUCKET_NAME}.s3.amazonaws.com'
AWS_S3_REGION_NAME = "<YOUR_AWS_S3_REGION_NAME>"
AWS_S3_SIGNATURE_VERSION = "s3v4"
AWS_QUERYSTRING_EXPIRE = 604800
CLOUDFRONT_DOMAIN = '<YOUR_CLOUDFRONT_DOMAIN>.cloudfront.net'

# Static
STATIC_LOCATION = "static"
STATIC_URL = f'{CLOUDFRONT_DOMAIN}/static/'
STATICFILES_STORAGE = 'django_static.storage_backends.StaticStorage'
```
 After that, run the
following command to collect static files:
```bash
$ python manage.py collectstatic
```

Verify that files are uploaded in S3, by checking up your S3 in AWS console or from terminal
### Verify that files are being served from CloudFront

Run the webserver:
```bash
$ python manage.py runserver
```
Visit `localhost:8000/admin` and see if the files are being served from CloudFront by checking the network request with Development tools:

![img.png](img.png)


## Improvements & What to do next
Improve the way that environment variables are being handled. </br>
For example, instead of hardcoding the AWS credentials in settings.py, we can use environment variables. </br>
```python
AWS_ACCESS_KEY_ID =os.environ.get('AWS_ACCESS_KEY_ID')
...
```

## Contact:

If you have any questions regarding the topic or anything else, feel free to reach to me on: </br>

* [LinkedIn](https://www.linkedin.com/in/valon-januzaj-b02692187/) </br>
* [Github](https://github.com/vjanz) </br>
* [Email](mailto:valon.januzaj98@gmail.com)

## License

This project is licensed under the terms of the MIT license.

