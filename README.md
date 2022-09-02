# 2022-09-enterprise-demo

[![Example Enterprise Workflow](https://github.com/pvnovarese/2022-09-enterprise-demo/actions/workflows/example_enterprise.yaml/badge.svg)](https://github.com/pvnovarese/2022-09-enterprise-demo/actions/workflows/example_enterprise.yaml)
[![Example Local Scan/SBOM Workflow](https://github.com/pvnovarese/2022-09-enterprise-demo/actions/workflows/example_local.yaml/badge.svg)](https://github.com/pvnovarese/2022-09-enterprise-demo/actions/workflows/example_local.yaml)
[![Codefresh build status]( https://g.codefresh.io/api/badges/pipeline/novarese/default%2F2022-09-demo?type=cf-1&key=eyJhbGciOiJIUzI1NiJ9.NjBiNmI3NmU2OTg1ODM3ZmU2ODZiNmE5.WZIffzq3OQPvPXy6pn1TbA4z9fMsdlS1U_cliZXbxKg)]( https://g.codefresh.io/pipelines/edit/new/builds?id=6312814a9935c4f0aa3af221&pipeline=2022-09-demo&projects=default&projectId=60b6b7aa4417e4bd7d843d0f)
[![CircleCI](https://dl.circleci.com/status-badge/img/gh/pvnovarese/2022-09-enterprise-demo/tree/main.svg?style=shield)](https://dl.circleci.com/status-badge/redirect/gh/pvnovarese/2022-09-enterprise-demo/tree/main)

Simple demo for Anchore Enterprise.

Includes workflow examples for Jenkins, CircleCI, Codefresh, Drone, and GitHub.

Partial list of conditions that can be tested with this image:

1. xmrig cryptominer installed at `/xmrig/xmrig`
2. simulated AWS access key in `/aws_access`
3. simulated ssh private key in `/ssh_key`
4. selection of commonly-blocked packages installed (sudo, curl, etc)
5. `/log4j-core-2.14.1.jar` (CVE-2021-44228, et al)
6. CVE-2021-3156 (sudo) provided via hints file (rpm also available)
7. added anchorectl to demonstrate automatic go module detection (new in syft 0.42.0)
8. wide variety of ruby, node, python, java installed with different licenses
9. build drift detection via baseline dockerfile with minimal packages/dependencies

