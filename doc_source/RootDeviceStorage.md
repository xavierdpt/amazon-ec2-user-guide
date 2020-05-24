
AMIs backed by Amazon EBS are recommended
instance store-backed instances do not support the Stop action

By default, the root volume for an AMI backed by Amazon EBS is deleted when the instance terminates.
Set the `DeleteOnTermination` attribute to `false` to keep it.

### Configuring the root volume to persist for an existing instance<a name="set-deleteOnTermination-aws-cli"></a>

To change the "DeleteOnTermination" status for an EBS volume on a running instance, the instance must be stopped first.
