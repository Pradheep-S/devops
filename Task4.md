# Configuring the Node port

service.yaml
```groovy
apiVersion: v1
kind: Service
metadata:
  name: my-app
  namespace: default
spec:
  type: NodePort  # Ensures external access via a specific port
  selector:
    app: my-app
  ports:
    - protocol: TCP
      port: 80       # Service port inside the cluster
      targetPort: 80  # The container's port
      nodePort: 30391   # Externally accessible port
```
![Screenshot from 2025-03-21 09-15-18](https://github.com/user-attachments/assets/7dac714f-eb87-4b91-ba87-d72d0371af2f)
