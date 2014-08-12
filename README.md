# Introduction

**Cron.pw** is a online service, which enables background processes for all ProcessWire sites. It also enables third party modules to take advantage of asynchronous task processing.

It is integrated into ProcessWire via this module.

You are able to perform up to 200 background tasks per day. If you need to perform more tasks per day, you are free to upgrade to **cron.pw unlimited**.
# Integrating PassiveCron in a ModuleTo see PassiveCron in a module, take a look at the [PassiveCronDemo](https://github.com/conclurer/PassiveCronDemo) module.
### Register the Module
Before creating background tasks you need to register your module at cron.pw. To do so, call the `registerModule()` method:
```
// Inside a module
$cron = $this->modules->get('PassiveCron');$cron->registerModule($this);```

`registerModule()` returns a boolean value. If the result is `true`, the module has been successfully registered at cron.pw. 

If returned `false`, the module is could not been registered. This can happen due to one of the following reasons:

- The module was manually disabled by the user
- The module was not authorized yet by the user


### Create Tasks

After being registered, one module can use PassiveCron's API to create background tasks.

Here are some examples for background tasks:

```$cron->addTask->in(1, 'hour')->run($this, 'methodToBeRun');```
This executes a method in one hour.
```$cron->addTask->next('hour')->every(1, 'hour')->run($this, 'methodToBeRun');```
This will run the method at the beginning of the next hour and will repeat it hourly.
```$cron->addTask->run($this, 'methodToBeRun', array('key' => 'value'));```
This will just run the method in the background while posting an array of parameters.

### Run Tasks & Return Values

When executed, the given method of your module will be executed.

```public function methodToBeRun(CronRequestExecution $execution, $parameters)
    {
        $execution->returnSuccess('000', 'Successfully completed', array('task' => 'exampleAsyncMethodA', 'key' => 'value'));
    }```
The method will receive the request execution object and an additional associative array of parameters.
The `returnSuccess()` method will send a custom status code back to cron.pw to be inspected. It's got the following parameters:
- A custom status code
- A custom status message
- Optionally, a associative array of additional data### More Information[Learn more about cron.pw](https://cron.pw)Please feel free to contact us for free additional testing volume or custom APIs at [developer@cron.pw](mailto:developer@cron.pw).