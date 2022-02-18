#add docker local images
docker-load:
	eval $(minikube docker-env)
# build the image
app-build: Dockerfile
	docker build --no-cache -f $< -t "obmovies_app:latest" .

# add to minikube
app-load:
	 minikube image load obmovies_app:latest

# deploy to minikube
app-deploy:
	kubectl apply  -f kubernetes/app-deployment.yaml

# delete the app from minikube
app-destroy:
	kubectl delete  -f kubernetes/app-deployment.yaml

	# deploy to minikube daemonset
app-ds:
	kubectl apply  -f kubernetes/app-daemonset.yaml

# build and deploy in one command with deployment and service
app-set-dpl:
	make docker-load && make app-build && make app-load && make app-deploy

	# build and deploy in one command with daemonset
app-set-ds:
	make docker-load && make app-build && make app-load && make app-ds


# run Tests
app-tests:
	export podobmovies=$(kubectl -n obmovies get pods | awk '{print $1}' | awk 'FNR == 2 {print}')
	kubectl -n obmovies exec --stdin --tty $(podobmovies) -- /bin/bash -c "pytest tests/test_paging.py && pytest tests/test_facets.py && pytest tests/test_user_management.py"
