# Problem
Application was showing build errors, dockerfile was using outdated image & was unoptimized.

## Root Cause
- Bad image. Outdated. was missing 4 years of security patches.
- Bad RUN commands. potential relibility issues.

## Solution
- Updated Dockerfile
- Used correct debian based image which is maintained.
- Optimized the docker build.

## Validation
- Application responds on port 5000
- Container builds successfully
- no buildtime errors

## Key Skills Demonstrated
- Docker debugging
- Docker build optimization