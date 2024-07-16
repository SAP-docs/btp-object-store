<!-- loioc3e904aa952c4301a711f77fb9aaa666 -->

# Retrieve Parameters Configured on Service Instance

The following command will retrieve all the paramters *preventDeletion* configured on a service instance:

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
   "preventDeletion": true
}
```

