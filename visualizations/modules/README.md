# Modules Folder

In this folder you can write individual modules for processing paros sensor data.

Each script should have a filename like:

```
<ORDER>_<NAME>.py
```

Where `<order>` is the order to be run relative to the other modules. For example, if you need to calculate FFT over time on data with DC offset removed data, you might have modules like `1_dcremove.py` and `2_fft.py`, where the `1_` will run first.

In each script you need to have one `main` method, which accepts 1 argument. **The naming of the argument matters!**

The argument should be named according to the data you are looking for. For example, if the input data you want is the raw data, the argument should be `datastream`, because that is the name of the bucket for raw data in influxdb. The main method should return the output data in a list of lists format:

```
[
    ["timestamp in ISO + Z", "value1", "value2", ..., "valueN"],
    ["timestamp in ISO + Z", "value1", "value2", ..., "valueN"],
    ...
]
```

Do not include the sensor ID in the output data, the method will be fed each sensor individually.