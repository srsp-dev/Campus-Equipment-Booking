# Campus Equipment Booking Service CIA
Java 17 / Spring Boot REST API for a CI/CD lab assessment.

## Build and test
`mvn clean test`

## Run
`mvn spring-boot:run` — port 8080.

## Endpoints
- `GET /api/equipment`
- `GET /api/equipment/{id}`
- `POST /api/bookings`
- `GET /api/bookings/{id}`
- `POST /api/bookings/{id}/cancel`
- `GET /actuator/health`


## Assigned Change Request

Fixed the inventory validation defect to prevent bookings from exceeding the available equipment quantity. Added tests for positive, zero, and negative quantities, exact inventory limits, overbooking, and ensuring rejected requests do not modify inventory.

## Docker

Build the Docker image:

    mvn clean package
    docker build -t campus-equipment-booking:set-e .

Run the container:

    docker run -d --name campus-booking-app -p 8081:8080 campus-equipment-booking:set-e

Verify the image and container:

    docker images
    docker ps

Health check:

    curl http://localhost:8081/actuator/health

## Kubernetes Deployment

Start Minikube and load the Docker image:

    minikube start --driver=docker
    minikube image load campus-equipment-booking:set-e

Deploy the application and service:

    kubectl apply -f deployment.yaml
    kubectl apply -f service.yaml

Verify Kubernetes resources:

    kubectl get nodes
    kubectl get deployments
    kubectl get pods
    kubectl get services

Scale to two replicas:

    kubectl scale deployment campus-equipment-booking --replicas=2
    kubectl get deployments
    kubectl get pods

Access the application:

    minikube service campus-equipment-booking --url

Append /actuator/health to the returned URL to check application health.

## Jenkins CI/CD

The Jenkinsfile defines pipeline stages for Maven testing, packaging, and Docker image building. Jenkins is configured to use the GitHub repository and the feature/positive-quantity-validation branch. A GitHub webhook can trigger the pipeline automatically when changes are pushed.

## Git Evidence

Display the current branch, commit history, and working-tree status:

    git branch
    git log --oneline -5
    git status
