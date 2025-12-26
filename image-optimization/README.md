# Problem
Docker image is too big in size and bloated. 

## Real-World Scenario
Clients report that image is insanely large after build.

## Root Cause
- Using massive base images.
- Installing unnecessary build tools.
- Not managing package manager cache. 

## Solution
- Using official lightweight images.
- Updated Dockerfile and used multi-stage builds.
- Verified container startup

## Validation
- Image is x150 times smaller (1.2gb to 15mb)
- image builds faster. Saving time.

## Key Skills Demonstrated
- Image optimization
- Multi-stage builds.
