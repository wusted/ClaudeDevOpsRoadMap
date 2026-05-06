# Module 02: Infrastructure as Code — Hands-On Exercises

## Module Repository: `terraform-aws-infra`

All deliverables for this module live in `repos/terraform-aws-infra/` and on GitHub at `github.com/<username>/terraform-aws-infra`. Create it with `/setup-repo` before starting Exercise 2.1.

The repo's README should describe it as a Terraform portfolio demonstrating production patterns: state management, modules, multi-environment, drift detection, and CI integration. Include AWS architecture diagrams.

Replace earlier exercise paths like `devops-lab/terraform/01-local/` with the in-repo equivalents (e.g., `01-local/`, `02-aws-basics/`, `modules/vpc/`, `envs/dev.tfvars`).

---

## Exercise 2.1: First Terraform Project (Local Provider)

**Objective**: Understand the Terraform workflow without cloud costs using the local and random providers.

**Context**: Before touching cloud resources, master the plan/apply/destroy cycle locally.

**Steps**:
1. Create `devops-lab/terraform/01-local/main.tf`
2. Use the `local_file` resource to generate a configuration file from variables
3. Use the `random_string` resource to generate a unique identifier
4. Define variables in `variables.tf`, outputs in `outputs.tf`
5. Run: `init` → `plan` → `apply` → modify → `plan` → `apply` → `destroy`
6. Examine the state file (`terraform.tfstate`) and understand its structure

**Validation**: Resources created, modified, and destroyed cleanly. Can explain what's in the state file.

---

## Exercise 2.2: AWS Free-Tier Infrastructure

**Objective**: Deploy real cloud resources using Terraform.

**Prerequisites**: AWS free-tier account, AWS CLI configured

**Steps**:
1. Create `devops-lab/terraform/02-aws-basics/`
2. Configure AWS provider with region variable
3. Deploy:
   - A VPC with 2 subnets (public/private)
   - Security group allowing SSH and HTTP
   - An EC2 t2.micro instance in the public subnet
4. Output the instance public IP
5. SSH into the instance to verify
6. Modify the security group, observe the plan diff
7. Destroy everything

**Validation**: Instance is reachable, plan shows correct diffs, clean destroy

---

## Exercise 2.3: Remote State and Modules

**Objective**: Set up remote state and refactor into reusable modules.

**Steps**:
1. Create an S3 bucket + DynamoDB table for state (can bootstrap manually or with a separate TF config)
2. Migrate Exercise 2.2's local state to remote backend
3. Refactor the VPC resources into a module: `modules/vpc/`
4. Refactor the EC2 resources into a module: `modules/compute/`
5. Create a root module that composes both
6. Deploy using the modular structure
7. Verify state is stored remotely and locking works

**Validation**: State in S3, lock in DynamoDB, modules are reusable with different variables

---

## Exercise 2.4: Multi-Environment Deployment

**Objective**: Deploy the same infrastructure to dev and staging using variable files.

**Steps**:
1. Create `envs/dev.tfvars` and `envs/staging.tfvars` with different values (instance size, naming)
2. Deploy to dev: `terraform apply -var-file=envs/dev.tfvars`
3. Deploy to staging with separate state (different backend key or workspace)
4. Verify both environments exist independently
5. Modify dev without affecting staging
6. Destroy both

**Validation**: Two independent environments, changes to one don't affect the other

---

## Exercise 2.5: Import and Drift Detection

**Objective**: Bring manually-created resources under Terraform management.

**Context**: In enterprise environments (like Oracle), existing infrastructure wasn't created with IaC. Import is how you adopt Terraform incrementally.

**Steps**:
1. Manually create an S3 bucket via AWS console
2. Write the Terraform resource block to match it
3. Use `terraform import` to bring it into state
4. Run `terraform plan` — it should show no changes
5. Modify the bucket manually in the console
6. Run `terraform plan` — observe the drift detection
7. Decide: apply to correct drift, or update config to match reality

**Validation**: Import succeeds, drift is detected and resolved

---

## Exercise 2.6: Terraform + GitHub Actions

**Objective**: Automate Terraform with CI/CD (connects to Module 04).

**Steps**:
1. Create `.github/workflows/terraform.yml`
2. On PR: run `terraform fmt -check`, `validate`, and `plan`
3. Post plan output as a PR comment
4. On merge to main: run `terraform apply -auto-approve`
5. Store AWS credentials as GitHub Secrets
6. Test with a PR that adds a new resource

**Validation**: PR shows plan output in comment, merge triggers apply, resources are created
