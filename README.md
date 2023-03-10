# 2023-03-demo

[![Enterprise Demo Setup Workflow](https://github.com/pvnovarese/2023-03-demo/actions/workflows/enterprise_demo_setup.yaml/badge.svg)](https://github.com/pvnovarese/2023-03-demo/actions/workflows/enterprise_demo_setup.yaml)
[![Example Enterprise Workflow](https://github.com/pvnovarese/2023-03-demo/actions/workflows/example_enterprise.yaml/badge.svg)](https://github.com/pvnovarese/2023-03-demo/actions/workflows/example_enterprise.yaml)
[![Example Local Scan/SBOM Workflow](https://github.com/pvnovarese/2023-03-demo/actions/workflows/example_local.yaml/badge.svg)](https://github.com/pvnovarese/2023-03-demo/actions/workflows/example_local.yaml)
[![CircleCI](https://dl.circleci.com/status-badge/img/gh/pvnovarese/2023-03-demo/tree/main.svg?style=shield)](https://dl.circleci.com/status-badge/redirect/gh/pvnovarese/2023-03-demo/tree/main)
[![Codefresh build status]( https://g.codefresh.io/api/badges/pipeline/novarese/2023%2F2023-03-demo?type=cf-1&key=eyJhbGciOiJIUzI1NiJ9.NjBiNmI3NmU2OTg1ODM3ZmU2ODZiNmE5.WZIffzq3OQPvPXy6pn1TbA4z9fMsdlS1U_cliZXbxKg)]( https://g.codefresh.io/pipelines/edit/new/builds?id=640baaa2866842ffa25cc6d9&pipeline=2023-03-demo&projects=2023&projectId=639a01e7aeb99143fd42ec8c)

Simple demo for Anchore Enterprise.

Includes workflow examples for Jenkins, CircleCI, Codefresh, Drone, and GitHub.

Partial list of conditions that can be tested with this image:

1. xmrig cryptominer installed at `/xmrig/xmrig`
2. simulated AWS access key in `/aws_access`
3. simulated ssh private key in `/ssh_key`
4. selection of commonly-blocked packages installed (sudo, curl, etc)
5. `/log4j-core-2.14.1.jar` (CVE-2021-44228, et al)
6. added anchorectl to demonstrate automatic go module detection (new in syft 0.42.0)
7. wide variety of ruby, node, python, java installed with different licenses
8. build drift detection via baseline dockerfile with minimal packages/dependencies
