# CNAB Duffle Demo 1

This is demo for creating a [CNAB](https://cnab.io/) bundle with [Duffle](https://github.com/deislabs/duffle).

## Build the packages

### Basics

* create a new repo
* clone the repo
* init a duffle bundle
* copy duffle bundle data to our repo folder

### Build

```bash
duffle build .
```

### Confirm

We can read our bundle information via the `duffle show` command.

```bash
duffle show cnab-duffle-demo-1:1.0.0 -r
```

Or we can list all of our bundles, to see if it was successfully added.

```bash
duffle bundle list
```

Which should result into something like below.

```bash
NAME              	VERSION	DIGEST                                  	SIGNED?
cnab-duffle-demo-1	1.0.0  	7951eaa84bff2679dc2f8b98ba3a6f7ec705d658	true
helloworld        	0.1.0  	947282206c8027106c8c33098203ae30034da415	true
```

### Install

```bash
duffle install demo1 cnab-duffle-demo-1:0.1.0
```

It will say the following: ```Error: bundle requires credential for kubeconfig```

Let's setup our credentials, see below how.

Assuming you've done so, we can now try to install again, this time referencing our credentials configuration with `-c demo`.

```bash
duffle install demo1 cnab-duffle-demo-1:0.1.0 -c demo1
```

### Credentials

As this demo requires the ability to issue `kubectl` commands to a Kubernetes Cluster, we need a working `kubeconfig`.

To do so, we have to configure duffle to use a kubeconfig ***credential***.

#### Define Kubeconfig credential

```json
"credentials": {
    "kubeconfig": {
        "path": "/root/.kube/config"
    }
}
```

#### Generating credentials

The following will create a new credentials file for our bundle (`cnab-duffle-demo-1`) with the name `demo1`.

```bash
duffle creds generate demo1 cnab-duffle-demo-1
```

Then, select the `file path` option in the "dropdown".
