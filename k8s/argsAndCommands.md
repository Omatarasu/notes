# args and commnds 

	FROM Ubuntu

	CMD ["sleep", "5"] # execute, when container started

	docker run ubuntu-sleeper

	FROM Ubuntu

	ENTRYPOINT ["sleep"] 

> docker run  ubuntu-sleeper 50


	FROM Ubuntu

	ENTRYPOINT ["sleep"]

	CMD ["5"] # default value

>docker run  ubuntu-sleeper

set another value

>docker run  ubuntu-sleeper 50 

	apiVersion: v1
	kind: Pod
	...
	spec:
  	  containers:
      - name: ubuntu-sleeper 
        image: ubuntu-sleeper
        command: ["sleep"] # ENTRYPOINT ["sleep"]
        args: ["10"] # CMD ["5"]