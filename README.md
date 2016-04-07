# λambdify - feel yourserlf like an AWS Lambda God

**lambdify** allows you to create AWS Lambda function directly from the python code.
Just like that:

install *lambdify*...
```bash
$pip install lambdify
```
...create AWS Lambda with 4 lines of code:
```python
from lambdify import Lambda


@Lambda.f(name='echo')
def echo(*args, **kwargs):
    return args, kwargs

echo.create()

if __name__ == '__main__':
    import getpass
    echo(msg='Hello, {user}!'.format(user=getpass.getuser()))
```

Now you can head over to your [AWS Lambda console](https://console.aws.amazon.com/lambda/) and behold your **echo** function

# The goal
Lambdify aims to unite convenient task queues API (i.e. [Celery](http://www.celeryproject.org/), [Hue](http://huey.readthedocs.org/en/latest/#huey-s-api), [RQ's @job decorator](http://python-rq.org/docs/)) with AWS Lambda service coolest features.

At present, there are some solutions, that allow you to create and deploy lambdas, like [Zappa](https://github.com/Miserlou/Zappa), [lambda-uploader](https://github.com/rackerlabs/lambda-uploader), [lambder](https://github.com/LeafSoftware/python-lambder) etc., but they still have limitations of not being able to interact directly with a python program. 
lambdify overcomes such limitations by using the following algorithm:

1. Serialize the callable with it's globals using [dill](https://github.com/uqfoundation/dill)

2. Upload the .lambda.dump file containing the serialized function along with the rest of the package

3. Special ```container.py``` module will look for the .lambda.dump file and inject deserialized function into it's namespace

4. ????

5. Profit

# Documentation
```python
>>>from lambdify import Lambda
>>>help(Lambda)
```

# TODO

- [ ] Tests
- [ ] Local modules dependencies
- [ ] Versioning
- [ ] InvocationType='Event'|'RequestResponse'|'DryRun'
- [ ] etc.

***P.S. Lambdify is a POC, and at the time allows your lambda to only use site-packages, all local files won't be packaged, so each user-defined dependency should be contained withing the same file.***

***P.P.S***

```python
contributions != lambdify.WELCOME and contributions == lamdbify.NECESSARY
```