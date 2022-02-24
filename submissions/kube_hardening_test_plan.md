# Kube Hardening Test Plan

## Overview

As an overview to our cluster workloads, we'll continue to run three clusters.  We use Infrastructure-as-code to stand up our clusters so each environment (`test`, `dev`, `prod`) are as similar as possible.  Anytime we do hardening steps, we deploy the change first to `test`, then to `dev`, then to `prod` in that order with appropriate tests in each case.

## How will the changes be tested? (How will we ensure changes don't negatively affect our cluster?)

As described above, all changes will be first deployed into our `test` cluster and always using Infrastructure-as-code.  This lets us deploy in a repeatable way.  If basic testing goes well in the `test` environment, then the hardening step will be deployed into our `dev` environment.  The `dev` environment has workload simulators to enable us to scale the amount of usage running to simulate production workloads.  The new hardening step will be tested here to verify it is appropriate even under production-like workloads.  This environment is also traced and monitored just like our `prod` instance (the `test` cluster is not).  Only when the step passes all these stages do they get deployed into `prod`.

## Can changes be safely rolled back?

Yes, all changes are made through IaaC scripts rather than manually so they are repeatable.  All IaaC scripts are entered into a configuration version control repository.  This allows easy rollbacks if we need to for any reason.  This combiend with the process described above gives us a strong chance of reducing issues in `prod` and maintaining our ability to roll back any issues if the need arises.
