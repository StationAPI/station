load('ext://restart_process', 'docker_build_with_restart')

allow_k8s_contexts('cloud_okteto_com')

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

k8s_yaml(['manifests/login/deployment.yml', 'manifests/login/service.yml'])
k8s_yaml(['manifests/gateway/deployment.yml', 'manifests/gateway/service.yml', 'manifests/gateway/ingress.yml'])
k8s_yaml(['manifests/session-cache/deployment.yml', 'manifests/session-cache/service.yml'])

