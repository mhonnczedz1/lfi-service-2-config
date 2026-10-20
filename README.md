# lfi-service-2-config

Kubernetes manifests, owned by the team. Each service here is one subscription
in lfi-infrastructure-gitops, at its own path:

    ./               team-2-service-2 (web-service)

Inside a service's directory:

    base/                          the service's own manifests
    <cluster>/<environment>/       one environment: env.yaml (ArgoCD finds it by
                                   this file) and kustomization.yaml
    denied-builds.yaml             builds that must never reach prod (a released
                                   service only)

CI writes `images[0].newTag` in <cluster>/dev/kustomization.yaml. A release
moves that tag to prod. An environment's env.yaml may set `overrides:`, limited
to the keys the service's profile allows.
