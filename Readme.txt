Setup:
	Copy docker-compose.yaml & docker-compose-build.yaml to root of all projects (parent of projects):
	/root-project/docker-compose.yaml
	/root-project/docker-compose-build.yaml
	/root-project/udagram-api-feed/
	/root-project/udagram-api-user/
	/root-project/udagram-frontend/
	/root-project/udagram-reverseproxy/

	Create images:
		# Make sure the Docker services are running in your local machine
		# Remove unused and dangling images
			docker image prune --all
		# Run this command from the directory where you have the "docker-compose-build.yaml" file present
			docker-compose -f docker-compose-build.yaml build --parallel
	
	Run containers:
		source udagram-api-user/set_env.sh
		docker-compose up
		or
		docker-compose -f ./docker-compose.yaml -f ./docker-compose-build.yaml up -d
		
		check:
			docker images
			docker ps -a
	
	URL:
		Local:
			frontend: http://localhost:8100/
			reverseproxy: http://localhost:8200/api/v0/feed
		Online:
			frontend: http://aa32ac9f7cc484111b836c37799d08e1-789740622.us-east-2.elb.amazonaws.com
			reverseproxy: http://a0f1c932dfa2b46818b37b4aeb9189b3-96121857.us-east-2.elb.amazonaws.com:8200/api/v0/feed
