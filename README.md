# mongodb-enterprise-advanced-4-stig baseline

InSpec profile to validate the secure configuration of MongoDB against [DISA's](https://public.cyber.mil/stigs/downloads/) MongoDB Enterprise Advanced 4.x Security Technical
Implementation Guide (STIG) Version 1, Release 2. (Applies to database versions 4, 5, 6, & 7)

## Getting Started

**For the best security of the runner, always install on the runner the _latest version_ of InSpec and supporting Ruby language components.**

Latest versions and installation options are available at the [InSpec](http://inspec.io/) site.

## Inputs: Tailoring Your Scan to Your Environment

To ensure the profile runs correctly in your specific environment, you need to configure the following inputs in an `inputs.yml` file. A template file named `inputs_template.yml` is provided to help you get started. More information about InSpec inputs can be found in the [InSpec Profile Documentation](https://docs.chef.io/inspec/profiles/).

### Example Inputs You Can Use

```yaml
# The username for the MongoDB administrative account.
mongo_dba: "root"

# The password for the MongoDB administrative account.
mongo_dba_password: "root"

# The hostname or IP address of the MongoDB server.
mongo_host: "localhost"

# The port number on which the MongoDB server is listening.
mongo_port: "27017"

# The database to authenticate against.
mongo_auth_source: "admin"

# The path to the Certificate Authority (CA) bundle file for SSL/TLS connections.
ca_file: "/etc/ssl/CA_bundle.pem"

# The path to the MongoDB SSL/TLS certificate key file.
certificate_key_file: "/etc/ssl/mongodb.pem"
```

## Running This Overlay Directly from Github

Against a _**locally-hosted**_ instance (i.e., InSpec installed on the target hosting the MongoDB database)

```sh
inspec exec https://github.com/mitre/mongodb-enterprise-advanced-4-stig-baseline/archive/main.tar.gz --input-file=<path_to_your_inputs_file/name_of_your_inputs_file.yml> --reporter=cli json:<path_to_your_output_file/name_of_your_output_file.json>
```

Against a _**docker-containerized**_ instance (i.e., InSpec installed on the node hosting the MongoDB container):

```sh
inspec exec https://github.com/mitre/mongodb-enterprise-advanced-4-stig-baseliney/archive/main.tar.gz -t docker://<instance_id> --input-file=<path_to_your_inputs_file/name_of_your_inputs_file.yml> --reporter=cli json:<path_to_your_output_file/name_of_your_output_file.json> --show-progress
```

### Different Run Options

[Full exec options](https://docs.chef.io/inspec/cli/#options-3)

## Running This Overlay from a local Archive copy

If your runner is not always expected to have direct access to GitHub, use the following steps to create an archive bundle of this overlay and all of its dependent tests:

(Git is required to clone the InSpec profile using the instructions below. Git can be downloaded from the [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) site.)

When the **"runner"** host uses this profile overlay for the first time, follow these steps:

```
mkdir profiles
cd profiles
git clone https://github.com/mitre/mongodb-enterprise-advanced-4-stig-baseline.git
inspec archive mongodb-enterprise-advanced-4-stig-baseline
inspec exec <name of generated archive> --input-file=<path_to_your_inputs_file/name_of_your_inputs_file.yml> --reporter=cli json:<path_to_your_output_file/name_of_your_output_file.json>
```

For every successive run, follow these steps to always have the latest version of this overlay and dependent profiles:

```
cd mongodb-enterprise-advanced-4-stig-baseline
git pull
cd ..
inspec archive mongodb-enterprise-advanced-4-stig-baseline --overwrite
inspec exec <name of generated archive> --input-file=<path_to_your_inputs_file/name_of_your_inputs_file.yml> --reporter=cli json:<path_to_your_output_file/name_of_your_output_file.json>
```

## Using Heimdall for Viewing the JSON Results

The JSON results output file can be loaded into **[heimdall-lite](https://heimdall-lite.mitre.org/)** for a user-interactive, graphical view of the InSpec results.

The JSON InSpec results file may also be loaded into a **[full heimdall server](https://github.com/mitre/heimdall)**, allowing for additional functionality such as to store and compare multiple profile runs.

## Authors

- Sean Chacon Cai - [seanlongcc](https://github.com/seanlongcc)

## Special Thanks

- Will Dower - [wdower](https://github.com/wdower)
