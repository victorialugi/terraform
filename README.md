# Домашнее задание к занятию "Хранение в K8s" - `Молоствов Андрей`


### Задание 1

```
mkdir -p k8s-storage-tasks
cd k8s-storage-tasks
nano containers-data-exchange.yaml
kubectl apply -f containers-data-exchange.yaml
kubectl describe pod -l app=data-exchange
kubectl logs -l app=data-exchange -c multitool --tail=5
kubectl get pv
kubectl describe pv local-pv
```
<img width="1057" height="573" alt="image" src="https://github.com/user-attachments/assets/a949e91a-e55f-4fcb-87b4-ef25cf7a6273" />

<img width="853" height="118" alt="image" src="https://github.com/user-attachments/assets/22be1568-3c0b-4adf-bc58-caaad9162151" />

### Задание 2

local-pv - созданный вручную, статус Available
pvc-dcd0e528... - автоматически созданный, статус Bound к PVC
PVC привязался не к local-pv, а к автоматически созданному PV потому что:

1)У автоматического PV storageClassName: standard (дефолтный)

2)У PV не указан storageClassName

3)PVC ищет подходящий PV, нашел стандартный и привязался к нему
```
nano simple-pv-pvc.yaml
kubectl apply -f simple-pv-pvc.yaml --validate=false
kubectl get pv,pvc,pods -l app=data-exchange-pvc
kubectl logs -l app=data-exchange-pvc -c multitool --tail=3
kubectl delete deployment data-exchange-pvc
kubectl get pv
kubectl describe pv local-pv
```
<img width="982" height="121" alt="image" src="https://github.com/user-attachments/assets/4bd72e15-2481-47e7-96f1-45c820b877a7" />

<img width="842" height="158" alt="image" src="https://github.com/user-attachments/assets/1b756821-eaa1-45c1-9b92-eb446b49ec94" />

<img width="1032" height="489" alt="image" src="https://github.com/user-attachments/assets/dd4bb117-d345-485e-a236-8b28aff0dabb" />

