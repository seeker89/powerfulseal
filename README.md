
# PowerfulSeal

[![Travis](https://img.shields.io/travis/bloomberg/powerfulseal.svg)](https://travis-ci.com/bloomberg/powerfulseal) [![PyPI](https://img.shields.io/pypi/v/powerfulseal.svg)](https://pypi.python.org/pypi/powerfulseal)

**PowerfulSeal** injects failure into your Kubernetes clusters, so that you can detect problems as early as possible. It allows for writing scenarios describing complete [chaos experiments](https://principlesofchaos.org).

<p align="center">
  <img src="docs/media/powerful-seal.png" alt="Powerful Seal Logo" width="150"></a>
  <br>
  Embrace the inevitable failure. <strong>Embrace The Seal</strong>.
  <br>
</p>


## Highlights

- works with `Kubernetes`, `OpenStack`, `AWS`, `Azure`, `GCP` and local machines
- `Prometheus` and `Datadog` metrics collection
- `yaml` [policies](https://bloomberg.github.io/powerfulseal/policies) describing chaos experiments
- multiple [modes](https://bloomberg.github.io/powerfulseal/modes)

## [Documentation](https://bloomberg.github.io/powerfulseal)

[Powerfulseal documentation](https://bloomberg.github.io/powerfulseal) is included in the docs directory. It can be hosted locally with jekyll by running jekyll serve from the docs directory.

## Hello world!

Just to give you a taste, here's an example policy. It will kill a single pod, and then check that the service continues responding to HTTP probes, to verify its resiliency to one of its pods going down.

```yaml
scenarios:
- name: Kill one pod in my namespace, make sure the service responds
  steps:
  # kill a pod from `myapp` namespace
  - podAction:
      matches:
        - namespace: myapp
      filters:
        - randomSample:
            size: 1
      actions:
        - kill:
            probability: 0.75
  # check my service continues working
  - probeHTTP:
      target:
        service:
          name: my-service
          namespace: myapp
      endpoint: /healthz
```

Assuming that's in `policy.yml`, you can run it like this:

```sh
powerfulseal autonomous --policy-file ./policy.yaml
```

[Learn more](https://bloomberg.github.io/powerfulseal).


## Read about the PowerfulSeal

- https://medium.com/faun/failures-are-inevitable-even-a-strongest-platform-with-concrete-operations-infrastructure-can-7d0c016430c6
- https://www.techatbloomberg.com/blog/powerfulseal-testing-tool-kubernetes-clusters/
- https://siliconangle.com/blog/2017/12/17/bloomberg-open-sources-powerfulseal-new-tool-testing-kubernetes-clusters/
- https://github.com/ramitsurana/awesome-kubernetes#testing
- https://github.com/ramitsurana/awesome-kubernetes#other-useful-videos
- https://github.com/dastergon/awesome-chaos-engineering#notable-tools
- https://www.linux.com/news/powerfulseal-testing-tool-kubernetes-clusters-0
- https://www.infoq.com/news/2018/01/powerfulseal-chaos-kubernetes
- [PowerfulSeal presentation at KubeCon 2017 Austin](https://youtu.be/00BMn0UjsG4)

---

## Footnotes

PowerfulSeal logo Copyright 2018 The Linux Foundation, and distributed under the Creative Commons Attribution (CC-BY-4.0) [license](https://creativecommons.org/licenses/by/4.0/legalcode).