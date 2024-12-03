# ECR Integration on AWS STS with the ECR located in the seperate account.
Here, the assumption is ROSA(Openshift), which is deployed in Account A, and AWS ECR in Account B
e.g Account A:- 012813163517  Account B:- 285849855719
Documentation use
- [1] https://docs.aws.amazon.com/IAM/latest/UserGuide/tutorial_cross-account-with-roles.html
- [2] https://cloud.redhat.com/experts/rosa/cross-account-access-openid-connect/
- [3] https://cloud.redhat.com/experts/rosa/ecr/

### Steps
 1. Create the ECR registry in AWS Account B following the documentation [3].
 2. Made the changes in the ECR permissions and add the policy for the ECR
  ```
  Amazon ECR > Private registry > Repositories > hello-ecr > Permissions > Edit Policy json
  Apply ECR_Permission.json
  ```
 3. Setup access cross AWS accounts using IAM roles using documentation [1]
 4. Apply the below policies on the ManagedOpenShift-HCP-ROSA-Worker-Role becuase here we are doing cross-account access by role instead of serviceaccount.
 ```
 Apply Worker_role_allow-assume-ecr-role-in-destination on a ManagedOpenShift-HCP-ROSA-Worker-Role
 Apply Worker_role_policy1 on a ManagedOpenShift-HCP-ROSA-Worker-Role
 ```
 5. Verify the success by following the documentation in the [3]
