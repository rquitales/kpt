---
title: "Init"
linkTitle: "init"
type: docs
description: >
   Initialize a package with a object to track previously applied resources
---
<!--mdtogo:Short
    Initialize a package with a object to track previously applied resources
-->

{{< asciinema key="live-init" rows="10" preload="1" >}}

The init command initializes a package with a template resource which will
be used to track previously applied resources so that they can be pruned
when they are deleted.

The template resource is required by other live commands
such as apply, preview and destroy.

### Examples

{{% hide %}}

<!-- @makeWorkplace @verifyExamples-->
```
# Set up workspace for the test.
TEST_HOME=$(mktemp -d)
cd $TEST_HOME
```

<!-- @fetchPackage @verifyExamples-->
```shell
export SRC_REPO=https://github.com/GoogleContainerTools/kpt.git
kpt pkg get $SRC_REPO/package-examples/helloworld-set@next my-dir
```

<!-- @createKindCluster @verifyExamples-->
```
kind delete cluster && kind create cluster
```

<!-- @installResourceGroup @verifyExamples-->
```
kpt live install-resource-group
```

{{% /hide %}}

<!--mdtogo:Examples-->

<!-- @liveInit @verifyExamples-->
```shell
# initialize a package
kpt live init my-dir/
```

{{% hide %}}

<!-- @removeInventoryTemplate @verifyExamples-->
```shell
rm -r my-dir
kpt pkg get $SRC_REPO/package-examples/helloworld-set@next my-dir
```

{{% /hide %}}

<!-- @liveInit @verifyExamples-->
```shell
# initialize a package with a specific name for the group of resources
kpt live init --namespace=test my-dir/
```
<!--mdtogo-->

### Synopsis
<!--mdtogo:Long-->
```
kpt live init DIRECTORY [flags]
```

#### Args

```
DIR:
  Path to a package directory.  The directory must contain exactly
  one ConfigMap with the grouping object annotation.
```

#### Flags

```
--inventory-id:
  Identifier for group of applied resources. Must be composed of valid label characters.
--namespace:
  namespace for the inventory object. If not provided, kpt will check if all the resources
  in the package belong in the same namespace. If they are, that namespace will be used. If
  they are not, the namespace in the user's context will be chosen.
```
<!--mdtogo-->