## k8s-kops

This is a templated version of `k8s`, `kops`-based cluster.


## Usage

First of all, you have to have `kops` installed. [[kops-installation]]
Then, you can fairly use the templated version of the cluster.

* Export `KOPS_STATE_STORE` environment variable:
```
export KOPS_STATE_STORE="s3://exampleenv-kops-s3
```


* Create a template from values:
```
kops toolbox template --fail-on-missing \
                      --format-yaml \
                      --template src/eu-west-1/templates \
                      --snippets src/eu-west-1/snippets \
                      --values values/cluster-exampleenv.yml \
                      > dist/clusters/cluster-exampleenv.yml
```

* Generate a cluster from template:
```
kops create -f clusters/cluster-exampleenv.yml
```



It is possible to use `Makefile` target:

```
make dist/clusters/cluster-exampleenv.yml
```

Be informed, please, that this target assumes equallity of `<cluster-name>`
between `dist/clusters/<cluster-name>.yml` and `values/<cluster-name>.yml`


## Contibution

Make sure all tests passes from:

```
make test
```

Its requirement is `pre-commit`.




[kops-installation]: https://github.com/kubernetes/kops#installing
