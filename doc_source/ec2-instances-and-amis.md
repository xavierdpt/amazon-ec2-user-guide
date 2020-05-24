AMI: Amazon Machine Image

- Amazon EC2 Instance Types
  https://aws.amazon.com/ec2/instance-types

Limit on the number of instances that can be running
- How many instances can I run in Amazon EC2
  https://aws.amazon.com/ec2/faqs/#How_many_instances_can_I_run_in_Amazon_EC2
  ACDGIMRTZ: 1152 vCPUs
  FGPX and Inf: 128 vCPUs

### Storage for your instance<a name="storage-options"></a>

root device

local storage volumes: instance store volumes
  block device mapping

Block Device Mapping
block-device-mapping-concepts.md

instance fails, or instance is stopped or terminated => the data on these volumes is lost

use Amazon S3 or Amazon EBS volumes for persistent storage

Consider creating a bastion security group

instance stopped =>
- normal shutdown
- stopped state
- Amazon EBS volumes remain attached
  - but new volumes can be attached or existing volumes can be detached
- no charge for stopped instance
- instance type can be changed while the instance is stopped
- storage is billed
- an AMI can be created from the stopped instance
- kernel, RAM disk, instance type can be changed

instance termianted =>
- normal shutdown
- root device volume is deleted
- attached Amazon EBS volumes are preserved by default
  - deleteOnTermination setting
- instance is deleted

prevent accidental termination: disable instance termination
- also turn on disableApiTermination
- behavior of the shutdown command:
  - instanceInitiatedShutdownBehavior: 'stop' or 'terminate'
    - Amazon EBS volumes for root device => default to 'stop`
    - instance\-store root devices =>  always terminated 

AMIs:
- *backed by Amazon EBS*
- *backed by instance store*

AMIs can be deregistered while instance are using them
