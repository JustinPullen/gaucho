Gaucho
===========================================

Gaucho is simply some Python scripts to access the 
[Rancher](https://github.com/rancher/rancher)'s API to perform tasks which
I need to have executed through my deployment workflow.

At this point, it does not contain much but it might grow as I get more 
requirements.

Contributions are welcome if you want to use it and add to it.

## Usage

Gaucho can be run directly on a command line provided you have Python installed
as well as the dependencies listed below.

It can also be run as a Docker container:

```
docker run --rm -it etlweather/gaucho query 1s245
```

### Rancher Host, Access Key and Secret

Gaucho needs to know the Rancher host and must be given an access key and access
secret to be able to interact with the Rancher's API. This can be done through
environment variables:

   - `CATTLE_ACCESS_KEY`
   - `CATTLE_SECRET_KEY`
   - `CATTLE_URL`

#### Rancher Agent Container

If you run Gaucho in a container on Rancher, rather than set the environment 
variables manually, use the following labels to have Rancher automatically do it
for you.

```
io.rancher.container.create_agent=true
io.rancher.container.agent.role=environment
```

See [Service Accounts in Rancher](http://docs.rancher.com/rancher/latest/en/rancher-services/service-accounts/)
for more information on this feature.

## Supported API

### query

```
Usage: ./services.py query [<service_id>]

Retrieves the service information.

    If you don't specify an ID, data for all services will be retrieved.

Options:

   --service_id  The ID of the service to read (optional)
```

### upgrade

```
Usage: ./services.py upgrade <service_id> [<start_first>] [<complete_previous>] [<imageUuid>] [<batch_size>] [<interval_millis>]

Upgrades a service

    Performs a service upgrade, keeping the same configuration, but
    otherwise pulling new image as needed and starting new containers,
    dropping the old ones.

Required Arguments:

  service_id   The ID of the service to upgrade.

Options:

   --start_first        Whether or not to start the new instance first before
                        stopping the old one.
   --complete_previous  If set and the service was previously upgraded but the
                        upgrade wasn't completed, it will be first marked as
                        Finished and then the upgrade will occur.
   --imageUuid          If set the config will be overwritten to use new
                        image. Don't forget Rancher Formatting
                        'docker:<Imagename>:tag'
   --batch_size
   --interval_millis

(specifying a double hyphen (--) in the argument list means all
subsequent arguments are treated as bare arguments, not options)
```

## Dependencies

 - requests
 - baker

