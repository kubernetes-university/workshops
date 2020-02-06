# Install KIND ([instructions](https://kind.sigs.k8s.io/docs/user/quick-start))

You need Docker desktop installed (Windows/Mac) or docker for Linux

Windows:

```powershell
curl.exe -Lo kind-windows-amd64.exe https://github.com/kubernetes-sigs/kind/releases/download/v0.7.0/kind-windows-amd64
Move-Item .\kind-windows-amd64.exe c:\some-dir-in-your-PATH\kind.exe
```

Mac (brew)

```bash
brew install kind
```

## Create a multinode cluster:

Create a file with this content:

`kind.yaml`
```yaml
kind: Cluster
apiVersion: kind.sigs.k8s.io/v1alpha3
nodes:
- role: control-plane
- role: control-plane
- role: control-plane
- role: worker
- role: worker
- role: worker
```

```
kind create cluster --config kind.yaml
```