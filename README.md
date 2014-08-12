# Introduction

**Cron.pw** is a online service, which enables background processes for all ProcessWire sites. It also enables third party modules to take advantage of asynchronous task processing.

It is integrated into ProcessWire via this module.

You are able to perform up to 200 background tasks per day. If you need to perform more tasks per day, you are free to upgrade to **cron.pw unlimited**.




// Inside a module


`registerModule()` returns a boolean value. If the result is `true`, the module has been successfully registered at cron.pw. 

If returned `false`, the module is could not been registered. This can happen due to one of the following reasons:

- The module was manually disabled by the user
- The module was not authorized yet by the user


### Create Tasks

After being registered, one module can use PassiveCron's API to create background tasks.

Here are some examples for background tasks:

```




This will just run the method in the background while posting an array of parameters.

### Run Tasks & Return Values

When executed, the given method of your module will be executed.

```
    {
        $execution->returnSuccess('000', 'Successfully completed', array('task' => 'exampleAsyncMethodA', 'key' => 'value'));
    }



- A custom status message
- Optionally, a associative array of additional data