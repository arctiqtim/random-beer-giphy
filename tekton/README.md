# hipster-source

```shell
kubectl apply -f -<< EOF
apiVersion: v1
kind: Secret
metadata:
  name: git-ssh
  namespace: beer
  annotations:
    tekton.dev/git-0: github.com
type: kubernetes.io/ssh-auth
data:
  # Generated by:
  # cat id_rsa | base64 -w 0
  # This deploy key has read-only permissions on github.com/knative/build
  ssh-privatekey: 
  # Generated by:
  # ssh-keyscan github.com | base64 -w 0
  known_hosts: Z2l0aHViLmNvbSBzc2gtcnNhIEFBQUFCM056YUMxeWMyRUFBQUFCSXdBQUFRRUFxMkE3aFJHbWRubTl0VURiTzlJRFN3Qks2VGJRYStQWFlQQ1B5NnJiVHJUdHc3UEhrY2NLcnBwMHlWaHA1SGRFSWNLcjZwTGxWREJmT0xYOVFVc3lDT1Ywd3pmaklKTmxHRVlzZGxMSml6SGhibjJtVWp2U0FIUXFaRVRZUDgxZUZ6TFFOblBIdDRFVlZVaDdWZkRFU1U4NEtlem1ENVFsV3BYTG12VTMxL3lNZitTZTh4aEhUdktTQ1pJRkltV3dvRzZtYlVvV2Y5bnpwSW9hU2pCK3dlcXFVVW1wYWFhc1hWYWw3MkorVVgyQisyUlBXM1JjVDBlT3pRZ3FsSkwzUktyVEp2ZHNqRTNKRUF2R3EzbEdIU1pYeTI4RzNza3VhMlNtVmkvdzR5Q0U2Z2JPRHFuVFdsZzcrd0M2MDR5ZEdYQThWSmlTNWFwNDNKWGlVRkZBYVE9PQo=
EOF

kubectl create secret docker-registry regcred \
                    --namespace beer \
                    --docker-server=registry-docker-registry.registry.svc.cluster.local:5000 \
                    --docker-username=admin \
                    --docker-password=Arct1q \
                    --docker-email="tim.fairweather@arctiq.ca"

kubectl apply -f -<<EOF
apiVersion: v1
kind: ServiceAccount
metadata:
  name: arctiqtim-git-ssh
  namespace: beer
secrets:
- name: git-ssh
- name: regcred
EOF
```