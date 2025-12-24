# Problem
Container is not staying alive and exiting due to CMD/Entrypoint misconfigurations.

## Real-World Scenario
Client runs container but it exits instantly. Application works locally but not in Docker.

## Root Cause
- CMD executes short-lived process. 
- ENTRYPOINT is misconfigured. 
- No long-running foreground process (PID 1 exits)

## Solution
- Updated Dockerfile
- Fixed CMD / ENTRYPOINT usage
- Ensured app runs in foreground.
- Verified container startup

## Validation
- Container stays alive (docker ps)
- Application accessible on port 8080
- Clean startup and shutdown behavior

## Key Skills Demonstrated
- Docker debugging & lifecycle management
- CMD vs ENTRYPOINT best practices
- Production-ready Dockerfile design