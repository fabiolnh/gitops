# GitOps (Currently Studying)

1) In a "normal life" you have:

    Code -> Git Repository -> CI -> CD -> K8S
   
- You do not have the confirmation that what you have in the Git Repository is what is running on your production environment
- If someone change the image in production, you will not have it synchronized with your git.
- How to guarantee that both are integrated?
  
2) With GitOps, you have a synchronization
- The idea is to work in a declarative way. (such as the terraform)
- The Git Repository is the center attention (guarantee that what is there is the production state)

    Code -> Git Repository -> CI -> CD -> Commit to Git informing the version in a declarative way (there is no communication with K8S here). This commit can be in the same repository or in another. Wesley usually uses another repository to do the commits. So, it is good to think about it)

- There is an Agent that will be "asking" to the Git Repository the current version. When the Agent recognizes the modification, the agent will change the version in the K8s
- If the agent see that there is a different version, it will recommend to synchronize (you can choose to synchronize automatically or manual)
- Good for Security: The CI/CD tool will not have access to the Cluster.
- Good for Developers: The developers can have access to the Agent to do Deploys and rollbacks
- The Kubernetes manifest (the image version) in git must be updated in every CD
- To update the file in git after the CD, use the tool : Kustomize
- The Agent will look every time to the kustomization.yaml
- OBS: In Wesley's Company, there is a unique repository with all the K8s manifests. So, instead of commiting in the same repository, it commits in this other repository. This way there are no commits ahead of others in the same repository. It is more organized. Think about it.

- Agent: ArgoCD (With it, you can see everything in real time, do rollbacks, etc).
- What I saw in course: In rollback, we do not update the git
- https://argoproj.github.io/cd/
