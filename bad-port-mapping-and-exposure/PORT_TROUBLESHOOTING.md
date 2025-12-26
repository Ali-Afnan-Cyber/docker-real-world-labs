# Port Access Troubleshooting Guide

## Problem: Cannot access containerized app from host

### Checklist:
1. ✓ App must listen on `0.0.0.0`, not `127.0.0.1`
2. ✓ Use `-p HOST_PORT:CONTAINER_PORT` when running container
3. ✓ EXPOSE in Dockerfile should match app's listening port
4. ✓ Container must be running (`docker ps`)
5. ✓ No firewall blocking the host port

### Debugging Commands:
```bash
# Check if container is running and ports are mapped
docker ps

# Check specific port mappings
docker port <container_name>

# View container logs for app startup
docker logs <container_name>

# Check what ports app is listening on inside container
docker exec <container_name> netstat -tlnp

# Test from inside container
docker exec <container_name> curl http://localhost:PORT
```

### Common Mistakes:
- Listening on 127.0.0.1 instead of 0.0.0.0
- Forgetting `-p` flag when running container
- Mapping wrong ports (check app's actual listening port)
- Firewall blocking host port
- App crashed inside container (check logs)

### Port Mapping Examples:
- `-p 8080:5000` → Host 8080 → Container 5000
- `-p 5000:5000` → Host 5000 → Container 5000
- `-p 3000:8080` → Host 3000 → Container 8080