# tekton-git-clone-ca

Openshift git-clone clustertask custom with self-signed CA.

The addition, apart from its parameterization, is the following:

```yaml
      volumeMounts:
        - mountPath: $(params.ca-truststore-path)
          name: ca-truststore
  volumes:
    - configMap:
        name: $(params.cm-ca-name)
      name: ca-truststore
```

You can add the CA to the cluster using the procedure: https://docs.openshift.com/container-platform/latest/networking/configuring-a-custom-pki.html

Or create the configmap for the namespace:

```bash
oc create configmap custom-ca-auto \
--from-file=ca-bundle.crt=</path/to/example-ca.crt> \
-n namespace
```
