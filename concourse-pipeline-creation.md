# Concourse pipeline creation

Below is some information to guide developers who are new to Concourse to get onboarded and create a pipeline.

## Onboarding

https://concourse-ci.org/quick-start.html

Concourse has a Command Line tool called Fly used to interact with the Concourse UI. Fly can be downloaded from the bottom right hand corner of the Concourse main page.

Go to Concourse and select your appropriate operating system.

This will download "fly.exe". Move it to a different folder and copy the path where you are storing the "fly.exe". Now open your system variables and edit the path.

Search for "Edit the system environment variables" in your local system.
Click on "Environment Variables"
Scroll down under System variables until you see "Path" and then select it and select "Edit"
Select "New" and paste the path where you saved your "fly.exe" file and then select "ok" in all the three windows.
To verify the Fly installation open a new command prompt and type fly -h. If you can see all fly help commands you are good.

## Pipeline requirements

Typical required jobs in an Angular app pipeline:
  - NPM audit (PR trigger)
  - Lint (PR trigger)
  - Unit test (PR trigger)
  - Prod build (PR trigger)
  - Sonar scan (PR trigger)
  - Create artifact (develop or main trigger)
  - Sonar scan develop (develop trigger)
  - Deploy (develop or main trigger)

Typical required jobs in an Angular library pipeline:
  - NPM audit (PR trigger)
  - Lint (PR trigger)
  - Unit test (PR trigger)
  - Prod build (PR trigger)
  - Sonar scan (PR trigger)
  - Create artifact and publish (develop or main trigger)
  - Sonar scan develop (develop trigger)

Typical required jobs in a Node.js microservice pipeline:
  - NPM audit (PR trigger)
  - Lint (PR trigger)
  - Unit test (PR trigger)
  - Prod build (PR trigger)
  - Sonar scan (PR trigger)
  - Create docker image with [security tool] scan (develop or main trigger)
  - Sonar scan develop (develop trigger)
  - Deploy (develop or main trigger)

Typical required jobs in a Spring Boot microservice pipeline:
  - Build and unit test (mvn clean package) (PR trigger)
  - Sonar scan (PR trigger)
  - Create docker image with [security tool] scan (develop or main trigger)
  - Sonar scan develop (develop trigger)
  - Deploy (develop or main trigger)

Typical required jobs in an Apigee proxy pipeline:
  - Unit tests (main trigger)
  - Create KVM artifact (main trigger)
  - Deploy KVM to Apigee (if not triggering a different deploy tool)
  - Create proxy artifact (main trigger)
  - Deploy proxy to Apigee (if not triggering a different deploy tool)
  - (Optional) Create Docker image for acceptance tests (test)
  - (Optional) Create Docker image for acceptance tests (stage)
