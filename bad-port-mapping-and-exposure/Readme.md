# Problem
Cannot access containerized app from host.

## Real-World Scenario
Clients report that they exposed the port but still can't access the app

## Root Cause
- Bad port mapping.
- App listening on localhost(127.0.0.1)
- Wrong usage of -p flag. 

## Solution
- Updated Dockerfile
- Updated Code. listening on 0.0.0.0
- Verified container listening on right port.

## Validation
- Container builds successfully and running with no errors
- Exposed on correct ports. Port mapping corrected and validated.

## Key Skills Demonstrated
- Docker debugging
- Port Mapping
