# Problem
Application works locally but fails inside Docker container due to missing environment varibles.

## Real-World Scenario
App not working properly on browser.

## Root Cause
- Missing environment variable

## Solution
- Updated Dockerfile
- Added Env variables.
- Verified container startup

## Validation
- Container builds successfully
- Application responds on port 5000

## Key Skills Demonstrated
- Docker debugging
- Container lifecycle management