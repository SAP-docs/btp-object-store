<!-- loio8b617c6ba2ba4660bd488927a64ffdfb -->

# Retrieve Parameters Configured on Service Instance

The following command will retrieve all the paramters *preventDeletion* & *versioning* configured on a service instance:

```
cf service <service_instance_name> --params
```

Alternatively, one can also use the following command:

```
cf curl "/v2/service_instances/<service_instance_guid>/parameters"
```

The `--params` flag is only available `cf8` onwards. If one is using an older version of cf & wants to retrieve parameters, use the alternate command as mentioned above.

Response of the get instance call:

```
{
   "preventDeletion": true,
   "versioning": false
}
```

