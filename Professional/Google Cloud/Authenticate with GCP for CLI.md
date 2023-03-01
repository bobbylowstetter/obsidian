## Authenticating with GCP and going to a specific project
- Run the command: `gcloud auth login`
- A browser window will open. Authenticate with your Google Account.
- Set your project with a similar command (not this exactly): `gcloud config set project PROJECTID`
## Going to a specific GKE (Google Kubernetes Engine) Cluster
- Run a similar command: `gcloud container clusters get-credentials NAMEOFCLUSTER --zone us-central1-c --project PROJECTID` 