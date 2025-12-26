Docker Image Optimization Guide

## Size Comparison Results
| Version | Size | Reduction | Vulnerabilities |
|---------|------|-----------|-----------------|
| Bloated | 1.2GB | Baseline | ~150 |
| Multi-stage | 15MB | 98.75% | ~20 |
| Optimized | 8MB | 99.33% | ~5 |

## Multi-Stage Build Strategy

### Pattern:
```dockerfile
# Stage 1: Build
FROM build-image AS builder
# ... build steps ...

# Stage 2: Runtime  
FROM runtime-image
COPY --from=builder /path/to/binary .
```

### Benefits:
- Removes build tools from final image
- Keeps source code out of production image
- Allows different base images for build vs. runtime
- Dramatically reduces size and attack surface

## Base Image Selection Guide

### For Compiled Languages (Go, Rust, C++):
1. **Build stage**: `golang:alpine`, `rust:alpine`
2. **Runtime stage**: `alpine`, `distroless/static`, `scratch`

### For Interpreted Languages (Python, Node):
1. **Build stage**: `python:3.11`, `node:20`
2. **Runtime stage**: `python:3.11-slim`, `node:20-alpine`

### Base Image Sizes:
- `ubuntu:22.04`: ~77MB
- `alpine:latest`: ~7MB
- `distroless/static`: ~2MB
- `scratch`: 0MB (empty)

## Build Optimization Flags

### Go:
```bash
CGO_ENABLED=0 go build -ldflags="-w -s" -trimpath
```

### Rust:
```bash
cargo build --release
strip target/release/binary
```

### Python:
```bash
pip install --no-cache-dir -r requirements.txt
```

### Node:
```bash
npm ci --only=production
```

## Layer Optimization Rules

1. **Order layers from least to most frequently changed**
```dockerfile
   # Good:
   COPY requirements.txt .
   RUN pip install -r requirements.txt
   COPY . .  # Changes frequently, goes last
```

2. **Combine RUN commands**
```dockerfile
   # Bad (3 layers):
   RUN apt-get update
   RUN apt-get install -y curl
   RUN rm -rf /var/lib/apt/lists/*
   
   # Good (1 layer):
   RUN apt-get update && \
       apt-get install -y curl && \
       rm -rf /var/lib/apt/lists/*
```

3. **Clean up in same layer**
```dockerfile
   RUN apt-get update && \
       apt-get install -y package && \
       apt-get clean && \
       rm -rf /var/lib/apt/lists/*
```