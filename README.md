# vconsole

Switch console between multiple communication devices (eg. serial / CAN bus / Ethernet).

## Functions

- Create console device(s).
- Switch console device(s).

## How to use

```c
/* callback function */
static rt_size_t outfunction(rt_device_t device, rt_uint8_t *buff, rt_size_t size)
{
    /* communication device should send the buff's data in this function */
}

/* create a console */
dev = vconsole_create("vc0", outfunction);
/* switch the console and return the old device */
old_dev = vconsole_switch(dev);
```

```c
/* switch back to the old device */
vconsole_switch(old_dev);
/* delete the console */
vconsole_delete(dev);
```

## API

`rt_device_t vconsole_create(const char *name, vc_output_t out)`

Create a console device object.

| parameter     | description                          |
| ------------- | ------------------------------------ |
| `name`        | device's name                        |
| `out`         | the callback function of data output |
| **return**    | **description**                      |
| `rt_device_t` | device object                        |

`rt_err_t vconsole_delete(rt_device_t device)`

Delete console device object.

| parameter  | description     |
| ---------- | --------------- |
| `device`   | device object   |
| **return** | **description** |
| `rt_err_t` | RT_EOK          |

> Only unused devices which are created by `vconsole_create()` function can be deleted

`rt_device_t vconsole_switch(rt_device_t device)`

Switch console between different communication devices.

| parameter     | description       |
| ------------- | ----------------- |
| device        | device object     |
| **return**    | **description**   |
| `rt_device_t` | old device object |

`rt_size_t vconsole_input(rt_device_t device, const rt_uint8_t *buff, rt_size_t size)`

Output data to the device object which are only created by `vconsole_create()` .

| parameter   | description         |
| ----------- | ------------------- |
| device      | device object       |
| buff        | data pointer        |
| size        | data size           |
| **return**  | **description**     |
| `rt_size_t` | data size in actual |
