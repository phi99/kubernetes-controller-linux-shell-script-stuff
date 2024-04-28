.***In Progress**

	 	 	   ----------------------------------------------------------------
	     	    	     ** Simple Kubernetes (k8s) Controller using shell script **
	  	 	   ----------------------------------------------------------------


```text
Mechanism/Functionality
------------------------
The controller watches events from the api server targetting change in configmap. When the annotation in configmap is modified with words that match with the label of the pod, the controller would request the list of pods containing that label to the api server, and then delete those pods.
```

```text
Implementation
---------------
1) Create service account
kubectl create sa <sa name> -n test-namespace
2) Create role (what actions are allowed)
apiVersion: 
kind: Role
metadata:
        name: 
        namespace: 
rules:
        - apiGroups:                - 
          resources:               - 
          verbs:
3) Bind the role to the created service account using role binding (who can perform the actions allowed in role (2))
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
        name: 
        namespace: 
roleRef:
        kind: Role
        name: 
        apiGroup: 
subjects:
        - kind: ServiceAccount
          name: 
          namespace: 


4) Create pod to use the created and binded service account

apiVersion: v1
kind: Pod
metadata:
        name: 
        namespace: 
spec:
        serviceAccountName: 
        containers:
                - name: 
                  image: 
                  imagePullPolicy: 
                  command:
                          - 
                          - 

5) Define variables to enable Curl to automatically include the cert of the CA in the request to check if the server's cert is signed by the CA, and token used to authenticate to API server.
export CURL_CA_BUNDLE=/var/run/secrets/kubernetes.io/serviceaccount/ca.crt
TOKEN=$(cat /var/run/secrets/kubernetes.io/serviceaccount/token)

6) Run the script

