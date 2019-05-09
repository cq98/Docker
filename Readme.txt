PART 1
Docker: develop, deploy and run applications with containers
- Image: executable package that includes everything needed to run an application
- Container: Runtime instance of an image [on Linux]
	- Show list of running containers: docker ps
- ls : list the files in the folder
- image ls: list the image details

PART 2
Dockerfile, app.py, requirements.txt
--tag : Shorcut: -t
- Run App [Mapped port 80 of the container to 4000]
	- curl http://localhost:4000
- Login: docker login [Auto-connect]
- Tag image in the format: docker tag image username/repository:tag
- PUSH into remote:
	docker push username/repository:tag
- PULL and run:
	docker run -p 4000:80 username/repository:tag

PART 3
Services: Different parts of the app, each service only runs one image. (one purpose)
- docker-compose yml

PART 4
Swarm: Deploy application into a cluster, run on multiple machines, join into a "Dockerized" cluster called a swarm.
- Manager: Can execute commands or authorize other machines to join the swarm as workers
- Worker: Provide capacity and do no have authority to command other machines
- docker swarm init: start swarm mode and current machine	
- docker swarm join on other machines: join the swarm as workers
- run VMs: myvm1 (tcp://192.168.99.100:2376), myvm2 (tcp://192.168.99.101:2376 )
- myvm1: manager 
	- docker-machine ssh myvm1 [Change to myvm1]
	- docker swarm init --advertise-addr 192.168.99.100:2376 [Make myvm1 the manager]
	- only manager can deploy
- myvm2: worker
	- docker swarm join --token SWMTKN-1-44iq42dodz8qh5dicr6rp63edbervjrjcg529g875u88lax448-eczcnsy1usuvp25e0ea77f0hv 192.168.99.100:2377 [*must be 2377 not 2376]
	2377 - port, 192.168.99.100 - myvm ip
- docker-machine ssh : que to VMs
- docker-machine ssh <VM> "Type command here"
- STUCK PART:docker stack deploy -c docker-compose.yml getstartedlab: Get image rejected, status is Shutting Down, have issues removing redundant stack, Solution: Look at the video below and follow how the person type, but yet to figure out how to remove redundant stacks

PART 5
Stack: Group of interrelated services that share dependencies and can be orchestrated and scaled together
- Add free visualizer service to docker-compose.yml
-
