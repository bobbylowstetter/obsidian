- Modify the record you want to make better. Example:
```
- context:
    cluster: gke_sdb-cloudinf-argocdpocca2e_us-central1_argocd-2-da9c5a7e
    user: gke_sdb-cloudinf-argocdpocca2e_us-central1_argocd-2-da9c5a7e
  name: gke_sdb-cloudinf-argocdpocca2e_us-central1_argocd-2-da9c5a7e
```
	Can be modified to be:
```
- context:
	    cluster: gke_sdb-cloudinf-argocdpocca2e_us-central1_argocd-2-da9c5a7e
	    user: gke_sdb-cloudinf-argocdpocca2e_us-central1_argocd-2-da9c5a7e
	name: argo2 <-----CHANGE OCCURRED HERE
```
		
- This will allow commands to be easier thrown. Example:
	- Instead of `kubectx gke_sdb-cloudinf-argocdpocca2e_us-central1_argocd-2-da9c5a7e` you can now do `kubectx argo2`