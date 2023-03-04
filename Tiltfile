load('ext://restart_process', 'docker_build_with_restart')

allow_k8s_contexts('admin@station-dev')

docker_build_with_restart('sthanguy/station-login',
							context='../station-login',
							entrypoint='go run main.go',
							dockerfile='../station-login/Dockerfile',
							extra_tag='latest',
							live_update=[
								sync('../station-login', '/home/nonroot/route'),
							]
)


docker_build_with_restart('sthanguy/station-gateway',
							context='../station-gateway',
							entrypoint='go run main.go',
							dockerfile='../station-gateway/Dockerfile',
							extra_tag='latest',
							live_update=[
								sync('../station-gateway', '/home/nonroot/route'),
							]
)

"""
docker_build_with_restart('sthanguy/station-image-bucket',
							context='../station-image-bucket',
							entrypoint='python3 main.py',
							dockerfile='../station-image-bucket/Dockerfile',
							extra_tag='latest',
							live_update=[
								sync('../station-image-bucket', '/home/nonroot/route'),
							]
)
"""

docker_build_with_restart('sthanguy/station-tag-aggregator',
							context='../station-tag-aggregator',
							entrypoint='gleam run',
							dockerfile='../station-tag-aggregator/Dockerfile',
							extra_tag='latest',
							live_update=[
								sync('../station-tag-aggregator', '/home/nonroot/route'),
							]
)



k8s_yaml(['manifests/login/deployment.yml', 'manifests/login/service.yml'])
k8s_yaml(['manifests/gateway/deployment.yml', 'manifests/gateway/service.yml', 'manifests/gateway/ingress.yml'])
k8s_yaml(['manifests/session-cache/deployment.yml', 'manifests/session-cache/service.yml'])
k8s_yaml(['manifests/tag-aggregator/deployment.yml', 'manifests/tag-aggregator/service.yml'])
# TODO: add image bucket here
